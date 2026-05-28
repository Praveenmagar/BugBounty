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