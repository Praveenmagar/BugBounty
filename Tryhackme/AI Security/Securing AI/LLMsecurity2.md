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