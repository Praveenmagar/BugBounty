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

## Why do many of these expose both HTTP and gRPC(gRPC Remote Procedure Call) at the same time?
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