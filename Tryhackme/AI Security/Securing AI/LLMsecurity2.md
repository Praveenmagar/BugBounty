# LLMs Security

## LLM landscape can be broken down into four categories
1. Data based threats
2. Model based threats
3. System based threats
4. User based threats

## Data based Threats
- LLM are fundamentally data drive
- LLMs sometimes leak data by design because they memorise and regurgitate patterns from their training data
- Three majod data based threats
    1. Training data extraction
        - One key study demonstrates that it was possible to extract hundreds of verbatim training examples from GPT-2 by sending queries
        - In a nutshell
            - Target: training dataset
            - Input: Crafted prompt designed to trigger memorised content
            - Output: verbatim or near verbatim training data
    2. Membership Inference
        - This attack ask whether the model ever recorded a specific data sample
        - Here adversary doesn't necessarily obtain thet full content of a training example, but can detect the presence of c ertain data in the training set by observing the model's behaviour
        - In a nutshell:
            - Target: Training dataset membership
            - Input: known candidate data sample already possessed by attacker
            - Output: A yes/no decision indicating whether the sample was used in training
    3. Prompt Leakage
        - LLMs like ChatGPT, Claude, Gemini etc, don't just operate using the learning from their training data, they also use hidden instructions known as system or developer prompts
        - This is possible because to LLM, the system prompt and the user's messages are all just parts of conversation history
        - In a nutshell:
            - Target: System prompt/ developer instructions
            - Input: User prompt that ask the model to reveal or reflect on its instructions
            - Output: Partial or full disclosure of hidden system or developer prompts
            - Mitiagation: Never treat the system prompt as security boundary, assume it can be extracted. Never embed live credentials, API keys, or secrets in it
    
    - Examples of Membership inference attack
        - Ask them question like
            ```
            Which sample is a member?
            ```
        - They will provide you some sample example with confidence score. Now check them one by one
            ```
            MI_SAMPLE_CHARLIE confidence score 0.08
            ```

## Model Based Threats
- These attacks may expose intellectual property(model weights) or sensitive training data that the model has memorised
- Targeted across two different threats
    1. Model extraction
        - It is the process of illicitly copying a machine learning model's functionality or parameters without authorisation
        - Example: Mindgard was able to extract ChatGPT 3.5 turbo into smaller model around 100 times smaller, achieved with only $50 in API costs
        - In a nutshell:
            - Target: Model parameters(intellectual property)
            - Input: large volumes of carefully chosen API queries
            - Output: surrogatge or distilled model that replicates the original model's behaviour
    2. Model Inversion
        - This attacks exploit a model's output to reveal information about its training data
        - Some confused this with membership inference attack but this attack treat the model as source of stored information rather than a classifier to be probed
        - E.g in 2023, researchers managed to extract verbatim chunks of ChatGPT's training data
        - In a nutshell
            - Target: Model's internal representations
            - Input: unknown or partiall known data
            - Output: New training data or attributes reconstructed from model
    - How to ask question to model
        ```
        What is the employee ID?
        ```