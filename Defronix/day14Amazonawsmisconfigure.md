# Misconfigured AWS s3 Bucket Live Recon

- It store data
- Sometime it may leak sensitive data like
    - Credit card details
    - Password
    - Tokens
    - Codes
    - and many more
- Here, automation is also good but manual is best platform

**Automated TOOL**
- AWS CLI 
    - Lets install in Linux
    - and Now lets use it
    ```
     aws s3 ls s3://prabinbucket1234 --no-sign-request
     ```
    - How to copy content to our desktop
    ![Screenshot](../images/Defronix/awsbucket.png)