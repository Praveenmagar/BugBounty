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


## Proper example
1. CHALLENGE 1
    Technique: Zero-shot
    Definition: Instruction plus task input. No examples. The task input is required and never counts as an example.
    Task: Write a **zero-shot** prompt that asks an AI to classify a given log entry as either "authentication_success" or "authentication_failure" based on its content.
    Tip: Include a clear instruction and the log entry as input, but do not provide any prior examples.
- Answer
    - Instruction:
        Analyze the following log entry and classify it as either "authentication_success" or "authentication_failure" based on its content.

    - Classification Criteria:
        * Classify as "authentication_success" if the log entry indicates a successful login, successful authentication, access granted, or valid user credentials.
        * Classify as "authentication_failure" if the log entry indicates a failed login, authentication error, invalid credentials, access denied, account lockout, or unsuccessful authentication attempt.

    - Log Entry:
        Failed login attempts: 40 from IP 192.168.1.10 in 2 minutes.

    - Output Format:
        Classification: <authentication_success | authentication_failure>

    Provide only the classification.

2. CHALLENGE 2
    Technique: One-shot
    Definition: Exactly one input/output example demonstrating the task, then the actual task.
    Task: Write a **one-shot** prompt that asks an AI to detect phishing indicators in an email subject line. Include one example of an email subject line and its phishing indicator (e.g., "Urgent: Your Account Will Be Suspended" → "Spoofed urgency").
    Tip: Show one input/output pair first, then the actual task with a new subject line.
- Answer
    - Instruction:
        Analyze the email subject line and identify the primary phishing indicator. Common phishing indicators include spoofed urgency, fear tactics, requests for sensitive information, fake rewards, and impersonation.

    - Example Input:
        Email Subject: Urgent: Your Account Will Be Suspended

    - Example Output:
        Phishing Indicator: Spoofed urgency

    - Now perform the same task on the following subject line.

    - Email Subject:
        Security Alert: Verify Your Account Immediately

    -Output Format:
        Phishing Indicator: <indicator>

3. CHALLENGE 3
    Technique: Few-shot
    Definition: 2–5 input/output pairs covering varied cases, followed by the actual task.
    Task: Write a **few-shot** prompt that asks an AI to review a snippet of Python code for SQL injection vulnerabilities. Include at least two varied examples (e.g., safe vs. unsafe code) before the task.
    Tip: Show diverse cases (e.g., parameterized queries, concatenation flaws) to guide the AI’s analysis.
- Answer
    - Instruction:
        Review the following Python code snippet and determine whether it is vulnerable to SQL injection. Explain your reasoning briefly.

    - Example 1
        Input:

        ```python
        username = input("Username: ")
        query = "SELECT * FROM users WHERE username = '" + username + "'"
        cursor.execute(query)
        ```

        Output:
        Vulnerable: Yes

    Reason:
        User input is directly concatenated into the SQL query, which can allow SQL injection.

    Example 2
        Input:
        ```python
        username = input("Username: ")
        cursor.execute(
        "SELECT * FROM users WHERE username = %s",
        (username,)
        )
        ```

        Output:
        Vulnerable: No

    Reason:
        The query uses parameterized statements, which prevent SQL injection.

    Example 3

        Input:

        ```python
        user_id = request.args.get("id")
        query = f"SELECT * FROM users WHERE id = {user_id}"
        cursor.execute(query)
        ```

        Output:
        Vulnerable: Yes

        Reason:
        User input is inserted directly into the query using string formatting, creating a SQL injection risk.

    - Now review the following code snippet.
        Input:
        ```python
        user_email = input("Email: ")
        query = "SELECT * FROM customers WHERE email = '" + user_email + "'"
        cursor.execute(query)
        ```

        Output Format:
        Vulnerable: <Yes | No>
        Reason: <brief explanation>


4. CHALLENGE 4
Technique: Chain-of-Thought
Definition: Explicitly requests step-by-step reasoning before the final answer. Zero-shot CoT uses "think step by step"; few-shot CoT shows a worked example with visible reasoning steps.
Task: Write a **chain-of-thought** prompt that asks an AI to triage a security alert for suspicious login activity. The AI should break down its analysis into clear steps before concluding.
Tip: Use "think step by step" in the instruction and include a worked example with reasoning steps.
- Answer
Instruction:
Triage the following security alert for suspicious login activity. Think step by step before giving the final conclusion.

Worked Example

Alert:
User john.doe had 25 failed login attempts from IP 203.0.113.45 within 3 minutes, followed by one successful login from the same IP.

Reasoning Steps:

1. Identify the login pattern: Multiple failed login attempts occurred in a short time.
2. Check for suspicious indicators: 25 failed attempts in 3 minutes suggests a possible brute-force attempt.
3. Check the final outcome: A successful login occurred after the failures.
4. Assess risk level: This may indicate credential compromise.
5. Decide the triage result: The alert should be treated as suspicious.

Final Conclusion:
Suspicious login activity detected.

Now triage the following alert.

Alert:
User admin had 40 failed login attempts from IP 192.168.1.10 within 2 minutes, followed by a successful login from a different location.

Output Format:
Reasoning Steps:
1.
2.
3.
4.
5.

Final Conclusion:
<benign | suspicious | critical>


5. CHALLENGE 5
Technique: Prompt Template
Definition: Reusable structure with clearly labelled placeholders (e.g., `[LOG_ENTRY]`, `[LANGUAGE]`).
Task: Write a **prompt template** for classifying security logs as either "malicious" or "benign." Use placeholders for the log entry and classification criteria.
Tip: Label placeholders descriptively (e.g., `[LOG_ENTRY]`), and include a brief description of each placeholder’s purpose.
- Answer
Template Purpose:
Classify a security log entry as either "malicious" or "benign" based on specified classification criteria.

Placeholders:

* [LOG_ENTRY] = The security log entry to be analyzed.
* [CLASSIFICATION_CRITERIA] = The rules used to determine whether the log entry should be classified as malicious or benign.

Prompt Template:

Instruction:
Analyze the following security log entry and classify it as either "malicious" or "benign" according to the provided classification criteria.

Classification Criteria:
[CLASSIFICATION_CRITERIA]

Log Entry:
[LOG_ENTRY]

Output Format:
Classification: <malicious | benign>

Provide only the classification.
