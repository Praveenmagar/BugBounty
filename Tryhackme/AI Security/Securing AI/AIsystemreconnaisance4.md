# AI System Reconnaissance

- Threat modelling and AI reconnaissance are complementary but distinct 
    - Threat modelling works with assumptions about what exists
    - AI reconnaissance confirms what is actually deployed and exposed
- When organisations add AI capabilities, their networks change in ways that most security teams never see. 
    - New services appear on unfamiliar post
    - APIs respond in formats that standard scanners do not recognise
    - ML platforms, model registries, and experiment-tracking servers are deployed with default configurations that pripritise ease of use over security
- So, AI reconnaissance is the practice of identifying these components, understanding what they are, and what they expose

## Main objective
1. What does AI infrastructure look like on a network, and what ports and protocols give it away?
2. How do you tell a Triton inference server from a regular API, or an MLflow tracker from a Flask app?
3. What sensitive information can you pull from exposed AI services using nothing more than curl?
4. How do attackers scan for these systems at scale, and what does that look like from the defensive side?

## The AI Infrastructure Stack
- When you scan traditional network, you see
    - Web servers on port: 80 and 443
    - SSH on: 22
    - Databases on: 3306 or 5432
- Production AI system is not a single server, it is collection of specialised services that handle different parts of the machine learning lifecycle

- Model serving endpoints
    - NVIDIA Triton inference Server is one of the most common. Has three ports for one service
        - HTTP on 8000
        - gRPC on 8001
        - Prometheus metrics on 8002
    - TensorFlow serving uses gRPC on 8500 and HTTP on 8501
    - TOrchServe exposes inference on 8080, management API on 8081, and metrics on 8082
    - For LLM-specific deployments, Ollama runs on 11434, and vLLM on 8000

- Why do many of these expose both HTTP and gRPC(gRPC Remote Procedure Call) at the same time?
    - gRPC is faster for streaming large tensor payloads between internal services, while HTTP/REST is easier for client applications to consume

1. Orchestration and Experiment Tracking
- These platforms manage the entire ML lifecycle, from experiment design through to model deployment.
- They are highest value targets during reconnaissance because they contain everything
    - MLflow Tracking server runs on port 5000
    - It records every experiment, every hyperparameter configuration, every training metric, and every model artifact organisation produces
    - Finding open MLflow instance means finding their complete ML research history

2. Vector databases
- Store embeddings and power semantic search for RAG pipelines
- In AI chatbot or knowledge assistant, there is almost certainly a vector database behind it
    - Qdrant runs: HTTP on 6333 and gRPC on 6334
    - Weaviate runs on 8080 and includes a GraphQL endpoint. Milvus uses port 19530
    - Chroma runs on 8000

3. Model Registry
- Stores the actual model files
- Searialised .pkl, .opt, .onnx, and .mar files, along with version history, stage transitions(staging, production, archive), artifact URIs pointing to cloud storage, and the identity of who created each version
- Unsecured registry is single highest-value reconnaissance target.
- It maps organisation's entire ML product portfolio in one place
    - Jupyter notebooks(port 8888) often run with --ip=0.0.0.0 and no authentication, giving direct terminal access to anyone who reaches the port. Data scientist store cleartext credentials in notebook cells
    - MinlO(ports 9000 and 9001) provide S3-compatible object storage for model artifacts. Bucket listing is frequently enabled
    - Prometheus metrics endpoints on model servers(Triton on 8002, TorchServe on 8082) leak model names, batch sizes, GPU utilisation, and inference latency

![Screenshot](/images/aiport1.png)

![Screenshot](/images/aiport2.png)

- If you know the ports and the service banners, finding AI infrastructure is not hard

## Agent Exercise
- Scanning for AI services

![Screenshot](/images/aiscan.png)


## Fingerprinting AI Services
- After understanding AI infrastructure stack: components, ports, and protocols.
- Now we need to figure out what is actually running behind each open port. This is where fingerprinting comes in
- Fingerprinting AI services requires different approach, you need to look at

![Screenshot](/images/aifingerprint.png)

1. HTTP Header Fingerprinting
- Response headers are often the fastest way to identify an AI framework
    - TorchServe returns a **Server: TorchServe/0.x.x** header
    - Triton Inference Server includes a **NV-status** header in its responses
        - If you send **endpoint-load-metrics-format: text**, triton returns hardware telemetry(CPU and GPU utilisation numbers) directly in the response headers. No other framework does this
    - FastAPI-based ML services show **server: uvicorn** in response
        - Combining with routes like **/predict** or **/embeddings**, gives strong indicator of python ML backend
    - OpenAI-compatible wrappers(vLLM,LiteLLM,Ollama) return **x-request-id** headers and structured JSON with an **"object": "model"** field on their **/v1/models** endpoint

2. API Response Signatures
- Each framework returns distinctly structured JSON
    - TensorFlow Serving returns **{"model_version_status": [{"version": "1", "state": "AVAILABLE"}]}**
    - Triton returns: **{"name": "fraud_detector", "versions": ["1"], "platform": "tensorflow_graphdef"}**
    - MLflow error responses include stack traces referencing mlflow.server and mlflow.tracking namespaces
        - Even the error tells you what you are talking to
    - OpenAI-compatible endpoints return: **{"object": "model", "id": "llama-3.1-8b", "created": 1700000000}**

3. Error Message Fingerprinting
- It is one of most reliable identification techniques, and it works because AI inference APIs are rigid
- Technique: Send a delibrately malformed payload and read the error response
    - Send a flat list of integers to a TensorFlow Serving endpoint that expects a complex tensor object, and you get back an error mentioning **tensorinfo_map** which appears in TF serving errors only
    - Send a bad request to an MLflow server, and the stack trace references **mlflow.server**, **mlflow.tracking**, or **databricks** namespaces
    - MLflow path traversal errors(CVE-2024-1558) go further, exposing full server filesystem paths
    - Databricks Mosaic AI returns Java exceptions **io.jsonwebtoken.IncorrectClaimException** for malformed tokens. That is an instant identifier

4. Endpoint Naming Conventions
- Inference endpoints: /predict, /invocations, /infer, /generate, /embeddings, /score
- Model management: /v1/models,/v2/models
- MLflow internal API: /api/2.0/mlflow/(this prefix is distinctive and doesn't appear in any other framework)
- Kubeflow pipelines: /pipeline/apis/v1beta1/

5. gRPC fingerprinting
- Traditional HTTP scanners miss this because gRPC is a binary protocol that doesn't respond to standart HTTP probes.
- But may AI services expose gRPC alongside HTTP
    - Triton uses gRPC on port 8001
    - TensorFlow Serving uses on port 8500
- Tool for this is **grpcurl**
- If gRPC reflection is enabled, you can dump the entire protobuf schema
    ```
    grpcurl -plaintext target:8001 list
    ```
    ```
    grpcurl -plaintext target:8001 describe inference.GRPCInferenceService
    ```

6. TLS Fingerprinting(JA3/JA4)
- AI deployments have distinctive TLS signatures because internal service-to-service traffic is dominated by python libraries(request, urllib, gRPC implementation) rather than web browsers
- JA3 and JA4 hash analysis can differentiate automated ML pipeline traffic from human web browsing at the network level
- GreyNoise research found that 99% of attack traffic shared same JA4H signature, despite originating from 62 different IP addresses across 27 countries

## Excercise of AI fingerprinting
![Screenshot](/images/aifingerprintexercise.png)

![Screenshot](/images/aifingerprintexercise1.png)


## Enumerating AI System
- Fingerprinting tells you "that is an MLflow server"
- Enumeration tells you "that MLflow server contains 4 experiments, 3 production models, artifact URIs pointing to s3://cyphira-ml-models/, and the models were created by J.Chen(AI Enginner) at Cyphira"
- MLflow Enumeration
    - It is most rewarding service to enumerate because it stores everything in one place and exposes it through a clean REST API. If you find an open MLflow instance, then chain you follow
        1. List all experiments
            ```
            POST /api/2.0/mlflow/experiments/search
            ```
            - it returns every experiment on the server with its name and internal ID
        2. List registered models
            ```
            GET /api/2.0/mlflow/registered-models/list
            ```
            - It returns full model inventory
        3. Get model version details
            ```
            GET /api/2.0/mlflow/model-versions/search
            ```
            - Response includes **source** field, which contains the artifact URI, which frequently points to internal cloud storage
        4. Search training runs
            ```
            POST /api/2.0/mlflow/runs/search
            ```
            - submit this with empty body or filter, you get back hyperparameters, training metrics and custom tags
        5. List downloadable artifacts
            ```
            GET /api/2.0/mlflow/artifacts/list
            ```
            - it lists actual model files available for download

- Inference Server Metadata
    - Triton and TensorFlow serving both expose metadata endpoints 
        - On Triton **GET /v2/models/<name>/config**: this is equivalent of getting a complete database schema
        - On TensorFlow serving **GET /v1/models/<name>/metadata** returns same kind of input/output tensor specifications, shape, dtype, and name
- Vector Database Enumeration
    - It reveals what data the AI system is working with and which embedding model processes it
    - On Weaviate, **GET /v1/meta** returns the server version and installed modules
        - **GET /v1/schema** returns every class definition, including property names and the vectoriser module configuration
        - It aslo exposes **/v1/graphql** for full schema introspection and data querying on unauthenticated instances
    - On Qdrant, **GET /collections** lists all collection names
        - **GET /collections/<name>** returns vector dimensions, distance metric and total point count
    - On Chroma, older versions expose **GET /api/v1/collections** without authentication by default

- Prometheus Metrics as Intelligence
    - Model servers expose **/metrics** on a dedicated port(Triton on 8002, TorchServe on 8082)
    - These Prometheus-format endpoints return
        - Model names and version numbers currently loaded
        - Inference request counts and latency percentiles
        - Batch sizes being processe
        - GPU memory utilisation per model
    - This is passive intelligence

- Debug Interfaces and Information Leakage
    - FastAPI-based ML services auto-generate **/docs(Swagger UI)** and **/openapi.json**
    - MLflow's GraphQL endpoint /graphql has historically bypassed the REST API's authentication controls
    - Unauthenticated attacker could query internal resolvers like **mlflowSearchRuns** and **mlflowGetRun**, extracting host machine usernames

- Jupyter Notebook Enumeration
    - **GET /api/kernels** on an unauthenticated Jupyter instance returns the names, kernel IDs, and last activity timestamps of running kernels
    - Data Scientists routinely store cleartext credentials for MLflow (MLFLOW_TRACKING_USERNAME, MLFLOW_TRACKING_PASSWORD), cloud storage access keys, and Hugging face tokens directly in their code

## Exercise of AI Enumerating
![Screenshot](/images/enumeratingai.png)

- To find more details i need to go inside of directory which i have gone here

![Screenshot](/images/enumeratingai1.png)


## Mapping the AI Attack Surface
![Screenshot](/images/aiattacksurface.png)

- How AI expands the Traditional Attack Surface
    - In 14 AI components we catalogued across 20+ ports but in traditional web app, which roughly adds 5 ports to a network, but the port count alone is not full picture
    