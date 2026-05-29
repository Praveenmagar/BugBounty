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
