# LLM foundation

## Understanding Token
- LLM doesn't read text way you do. When you type "hello, how are you?" 
- Model breaks into token " the smallest units it can understand" .
- Token are roughly equivalent to 3 to 4 characters, means most english are 1 to 2 tokens
- Example: Chatgpt become "Chat" + "gpt", here "chat" is one token and "gpt" is another
- Model convert token into unique number 
    - like "hello, how are you?" becomes [1256, 456,556,789]
- Different models use different tokenisation methods: GPT uses Byte-Pair Encoding, while BERT uses WordPiece


## Determinism vs nondeterminism
- Nondeterminism:
    - LLM will produce different output even with identical input which is called nondeterminism

- Determinism:
    - Same input always produce same output

- Context window: Its maximum "working memory" measured in token

- We can use different parameter to control model behaviours like
    1. Temperature: The randomness dial
    2. Max tokens: Length Limiter
        - It caps how long the response can be
        - 1 token roughly equal to 0.75 english words
        -  Set this too low and the model cuts off mid-sentence. Set it too high and you pay for rambling you don't need
        - Common token budgets:
            - Quick answers or tight summaries: 50 - 150 tokens
            - Detailed explanations: 500 - 1000 tokens
            - Full articles or reports: 2000+ tokens
    3. Top-p: Alternative randomness dial
        - It is temperature cousins
        - In general, it is advised to adjust temperature OR top-p, but not both

## Anatomy of Prompt
- Good prompt aren't magic, they're carefully structured instruction that guide model towards desired outcome
- Four pillar of effective prompt
    1. core instruction:
        - provide clear instruction set which direct AI focus
        - Dont say "Help me with cooking". Instead use clear instruction "Draft a 300-word social media post about a new eco-friendly product aimed at millennials"
    2. Relevant context: 
        - Background information which helps to understand situation and perspective
        - Here try to style role " You are an experienced marine biologist specialising in fish"
    3. Desired output format: 
        - stating format/structure and length make the response immediately useful
        -  For example, "Summarise these 3 log samples each in a bullet point, all under 50 words".
    4. Constraints: 
        - rules or limit which keep AI on track and avoid unwanted directions
        - For example, "Write an academic report on IoT devices, provide citations in MLA format, and include a bullet-pointed summary section at the end (do NOT exceed 5 bullets)"

## Specificity vs Verbosity
- Clear, specific prompt generally yield better results, but overly wordy prompt confuse model
- Aim for sweet spot, provide enough detail to remove ambiguity
    - Too Vauge: 
        - "Write a function to handle user data." 
        - This gives almost no guidance
    - Too verbose: 
        - "Write a function that takes user data which could be an object or maybe an array… validate it but also maybe transform it and handle errors but I don't know what kind of errors, just make it work and also it should be fast and clean and... Etc."
        - This buries the task in rambling, unclear instructions.
    - Just right: 
        - "Write a JavaScript function that: (1) takes a user object with name, email, and age; (2) validates that email is properly formatted; and (3) returns the validated object or throws an error listing the validation failures."
        - Concise and specific


## System Vs User Prompt
- Instruction hierarchy "System prompt set the rules, user prompt provides the questions, and the model follows the system's constraints while answering the user"

![Screenshot](/images/systemprompt.png)

- Regardless of whether something is labelled "system", "developer", or "user", the model ultimately sees a single sequence of tokens
-  The model learns to respect role labels and priority markers during training, but this respect is probabilistic, rather than guaranteed.

- Why this matter for security?
    - The foundation for attack surface is that when system and user input merge into a single text stream, clever person can craft user input that mimics or conflict with system instruction

![Screenshot](/images/systemprompt1.png)


## Advanced Prompt Technique
- Shot specturn
    - shot refers to training examples you provide within your prompt
    - Different types of shot
        1. Zero-shot:
            - Prompt gives a model task with no examples, relying entirely on its pre-trained knowledge
        2. One-shot:
            - Provides a single example to clarify expectations
        3. Few-shot:
            - Include 2 to 5 examples so model recognises pattern

    ![Screenshot](/images/shot.png)

- Chain of Thought(CoT)
    - Introduced by Google researchers in 2022, CoT asks model to break down complex task into intermediate steps, mimicking how humans solve multi-step problems

- Prompt Template:
    - Templates are standardised prompt structure for recurring task
    ![Screenshot](/images/prompttemplate.png)

- When to Use
    - Zero-shot: Simple, well-defined tasks where instructions are clear
    - One-shot: Format clarification or style guidance needed
    - Few-shot: Complex patterns, domain-specific outputs, multiple edge cases
    - Chain-of-Thought: Multi-step reasoning, security analysis requiring justification, debugging complex logic
    - Templates: Repeatable tasks, team standardisation, quality control
