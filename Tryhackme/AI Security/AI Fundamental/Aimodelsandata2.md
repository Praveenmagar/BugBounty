# AI Model and data

## Where does data come from?

![Screenshot](/images/AImodel1.png)


## The problem of Provenance
- Data provenance is the ability to answer three questions about any training data
    1. Where did it come from?
    2. When was it collected?
    3. Has it been modified since?

-  SolarWinds taught the industry that you can't trust a compiled binary if you don't know what went into it, which is exactly why software bills of materials (SBOMs) became standard practice. 
- The AI equivalent is the ML-BOM(Machine Learning Bills of Materials): a documented inventory of dataset sources, licenses,PII categories, and filtering decisions.

## Building the model
- Epochs
    - An epoch is one complete pass of the training algorithm through the entire dataset
    - In practice, models are trained over many epochs.
    - The algorithm repeatedly sees the same data, adjusting its parameters each time until it converges on accurate predictions.

- Overfitting
    - More epochs don't always make better model
    - When training for long time model stop learning and start memorising training data, this problem is called overfitting
    - Overfit model perform well on its training data but poor in new data
    - This type of model can reproduce sensitive training data when prompted causing security issue

- Model validation
    - Validation set
        - To detect overfitting early, set of training data is held back and never used for training, this is validation set
        - If training accuracy increases but validation accuracy drops, thats overfitting
        - validation is quality gate, model who skip this result unknown behaviour resulting security risk

- Post training optimisation
    - After Completing training, model often goes through compression steps before deployment. Two most common are
        1. Pruning : Remove parameters that contribute little to predictions, shrinking model size
        2. Quantisation: Reduces numerical precision of weights(32 bits to 8 bits floats) to cut memory and compute requirements
    
    - Research show after quantisation reduces safety mechanism
    -  When an organisation downloads a quantised model without documentation of what changed during compression, they're inheriting unknown behaviour modifications alongside efficiency gains.

- Federated Learning
    - In training model, all data flows into single central location
    - But, in federated learning model is trained across different decentralised devices or orgainzations, with each training locally on their own data and only sending weight updates back to central server for aggregation
    - This was designed with privacy in mind. A hospital sharing patient records to train a model is a data protection problem; a hospital contributing model updates without ever sending the records is a much easier conversation
    - Here if local update poisoned weight then it creates problem
    - So, this solve privacy problem but creates another problem


## Inheritance Problem
- Traning LLM from scratch means 
    - assembling trillions of tokens of data
    - acquiring compute infrastructure to process it
    - running training job cost tens of millions of dollar
- So, best start with others model

- Pre-trained model and fine- Tuning
    - Fine tuning is the process of continuing to train one of these pre-trained models on smaller, task specific datasets

    - When you fine tune trained model, you inherit everything that model already contain which result in
        1. safety alignment erodes, not brakes: example model has been trained to follow safe path when generating response. Fine tuning is like adding new path
        2. Specialisation increases attack surface: fine tuning narow focus, reducing resilience to unexpected tokens
        3. Version matters, and it's rarely tracked 



## Black Box Problem
- When security team want to audit software they can
    - read source code
    - compiled binaries can be disassembled, stepped through, and reason about
- In Trained model
    - they're billions of floating-point number
    - they carry no human readable record of
        - how they are shaped?
        - what data influenced them?
        - what behaviours they encode?

## Model card
- It is structured document that accompanies model and describe what it is, how it was built, and where it falls.
- It was introduced by google researcher in 2019

![Screenshot](/images/modelcard.png)

- The GAP
    - Like in mango juice there is very low percent mango included, in model also there's no regulatory requirement to produce one; as of now, it remains voluntary for most use cases
    -  The Data Provenance Initiative audit of over 1,800 datasets found documentation gaps throughout the supply chain, and model cards sit at the end of that same underdocumented pipeline.
