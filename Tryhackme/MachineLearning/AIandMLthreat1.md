# AI and ML security Threat

## Machine learning life cycle
- It remains an iterative process

![Screenshot](/images/ml.svg)

## Machine learning algorithm
- It is mathematical methods used to learn patterns from data
- It consists of three key components
    1. Decision process: make predictions or classification based on input data
    2. Error Function: Evaluates performance and provides feedback
    3. model optimisation process: it fine tunes the algorithm to minimise errors and improve accuracy
- ML algorithm falls into four categories
    1.  Supervised learning
    2. Unsupervised learning
    3. Semi-supervised learning
    4. Reinforcement learning


## Neural Network and Deep learning
- Neural network enable computers to behave like humans
- Human brain processes information using interconnected neurons, which communicate with each other using synapses.
- Synapses allow the brain to send electrical/chemical signals from neuron to neuron

![Screenshot](/images/neuralnetwork.svg)

- Each node represents a neuron, and connections between them act as synapses.
- The hidden layers process and refine the input, bringing the network closer to a prediction. 
- Each connection has a weight, determining its importance
- for example, in email classification, the body text might have more weight than the subject line
The output layer then produces the final prediction

- ML need labeled data
- A Deep Learning(DL) algorithm can take unlabelled, unstructured raw data and determine its key features, which separate it from other categories, this means DL doesn't require human interaction and, in that way, is self-learning.


## Large language Model(LLMs)
- They are deep learning-based models that can process and generate text by predicting the next word
in a sequence
- They are first trained in a "pre-training" phase, where they process vast amounts of text, GPT-3 alone was trained on data that would take a human 2,600 years to read nonstop
- Instead of relying on labelled data, LLMs use billions of parameters that function like puzzle
pieces, enabling them to understand and generate human-like language when assessed together.
- They begin by generating a word at random to finish the text:
- The guess is then compared with what the correct final word actually was, and the parameters are fine-tuned to make it more likely to predict what, in fact, was the right word until the model can accurately predict the correct word to end the sentence (and less likely to choose the incorrect words) using an algorithm called **backpropagation**
- Now imagine this process happening trillions of times, repeating this process over and over again until it can not only predict the end of the training data but also raw unseen data. This only possible due to advancements in hardware, like GPUs (Graphics Processing Units), enabling masses of parallel operations and processing of large datasets as well as advancements in neural networks, specifically a type of neural network called **transformer neural networks**.
- Neural network: process one data at a time
- Transformer neural network: Process multiple data at a time
- After the pre-training, humans come back into play, performing a step called RLHF (Reinforcement Learning from Human Feedback)

![Screenshot](/images/llms.svg)
