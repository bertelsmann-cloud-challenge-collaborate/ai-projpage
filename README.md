# Udacity Bertelsmann Technical Scholarship Cloud Track Challenge Project - Deploy An AI Sentiment Prediction App to AWS Cloud
This repo is the project page of the 3 project repos and contains information about the project.
 ---
#### _The project was created by 3 scholars from the Cloud Track Challenge_

![png](assets/BertelsmannChallenge.png)

## Project Artifact Repositories
The project has 3 code and artifact repositories:
### [ai-frontend](https://github.com/bertelsmann-cloud-challenge-collaborate/ai-frontend)
> * This repo contains the project website static files **_index.html_** and **_app.js_**
>
> * The files reside in the **_static_** folder, any changes pushed onto the master branch will trigger the GitHub CI/CD Action on the repo to copy the 2 static files to the S3 bucket hosting the project website on AWS

### [ai-automation](https://github.com/bertelsmann-cloud-challenge-collaborate/ai-automation)
> * This repo contains the Serverless Framework configuration file **_serverless.yml_** and Lambda function code files for deployment of Lambda functions, their triggering events and required infrastructure resources (e.g. DynamoDB, S3) to AWS.
>
> * Any changes pushed to the master branch will trigger the Github CI/CD Action on the repo to deploy the changes to AWS

### [ai-backend](https://github.com/bertelsmann-cloud-challenge-collaborate/ai-backend)
> * This repo contains the code files for building and pushing a Flask docker image to ECR, then deploying a new task definition to ECS
>
> * Any changes pushed to the master branch will trigger the Github CI/CD Action on the repo to apply and deploy the changes to AWS

## Project Information
The project transforms the original infrastructure of a RNN sentiment prediction app to an AWS cloud deployable infrastructure.

**Project Goals**: Implements various AWS cloud stack concepts covered in Phase I of the scholoarship challenge, namely Lesson 12 thru 23, plus additional advanced concepts such as Serverless Framework, CI/CD, Docker, API Gateway, ECS, ECR, DynamoDB and Microservices.

**Project Team**: an international team with 3 members from Phase I of the Cloud Track Challenge:
* [Adrik S](https://github.com/Adriks976) (France)
* [Audrey ST](https://github.com/atan4583) (Australia)
* [Christopher R](https://github.com/christopherrauh) (Germany).

### RNN Sentiment Prediction App Original Infrastructure (Logical View)
![png](assets/architecture-orig.png)
#### The original architecture of the AI app consists of
> * a Flask app backend hosting a RNN sentiment prediction model
>
> * a website with a Vue Web UI powered by **_Springboot Framework_**
>
> * a datastore built on MySQL DB
>
> * It is styled in Microservices fashion. This makes the infrastructure and its underlying components easily transformable to AWS cloud deployable infrastructure
>
>
### RNN Sentiment Prediction App Transformed Cloud Infrastructure (Logical View)
![png](assets/architecture-cloud.png)
#### The transformation resulted in a streamlined infrastructure as below:
> * the Flask backend now runs in a docker container and utilizes AWS ECS
>
> * the website is now hosted on S3 bucket powered by AWS Lambda functions
>
> * the MySQL datastore is now replaced by a light weight noSQL DynamoDB
>
> The new AWS cloud infrastructure comes with these benefits:
> * costly specialist support effort in  Springboot, MySQL, Infrastructure resource deployment & provisioning no longer needed
>
> * built-in auto failover and user demand driven infrastructure scaling features
>
> * predictable operation performance with minimum effort and improved overall user experience
>
>
### RNN Sentiment Prediction App on AWS Cloud Infrastructure (Physical Implementation)
![png](assets/RNNappOnAWS.png)
#### Cloud Lesson Concepts Implemented
> * GitHub:  Lesson 1 - 12
>
> * AWS S3 Static Website: Lesson 14, 23
>
> * AWS Lambda function: Lesson 13
>
> * AWS Elastic Load Balancer: Lesson 16, 20
>
> * AWS Auto Scaling Group: Lesson 20
>
> * AWS Cloudformation: Lesson 19
>
> * AWS IAM: Lesson 15
>
 ---
#### Advanced Concepts Implemented
> * GitHub CI/CD workflow pipelines
>
> * AWS API Gateway
>
> * AWS ECS (elastic container service)
>
> * AWS ECR (elastic container registry)
>
> * Flask Docker (scaling between 1 to 3 instances)
>
> * AWS DynamoDB
>
> * AWS Serverless Framework
>
> * Microservices
>
>
### Workflows of the DevOps Model built on Serverless Framework and AWS Services
#### Workflow I
> * DevOps team merges feature branches to the master branch in 1 of the 3 GitHub repositories
>
> * Pushes to the relevant remote master branch
>
 ---
#### Workflow II
> * Code build process via 1 of the 3 build paths based on the repo receiving the push:
>
>  * If the push is onto **ai-frontend** repo, CI/CD Action **_Upload Website_** automatically runs to upload updated static files (index.html, app.js) to AWS S3 website **udacity-ai-frontend**
>
>  * If the push is onto **ai-backend** repo, CI/CD Action **_Deploy to Amazon ECS_** automatically runs to build a new Flask container to push to the ECR, then deploy a new task definition to the ECS on AWS cloud
>
>  * If the push is onto **ai-automation** repo, CI/CD Action automatically runs a serverless.yml configuration file to deploy Lambda functions, their triggering events and required infrastructure resources (e.g. DynamoDB, S3) to AWS and rebuild the website
>
 ---
#### Workflow III
> * Sentiment Prediction App Usage Scenarios
>
>  * User submits a sentiment prediction request thru S3 website **udacity-ai-frontend** and receives a prediction result
>
>     - User approves the prediction result, the approved result is written to the DynamoDB
>
>     - User revises the prediction result, the revised result is written to the DynamoDB
>
>  * User downloads prediction results in the DynamoDB as a CSV (This will be used as a new dataset for re-training of the RNN model)
>
 ---
#### Workflow IV
> * Depending on user usage demands on Sentiment Prediction App, AWS ECS and Auto Scaling group orchestrate to scale up to 3 Flask container instances to optimize workload distribution and app response time
>
>
### RNN Sentiment Prediction App Use Case Demo
#### Scenario I
![png](assets/UC1a.png)
> 1. User enters a text in the web UI and click Submit to get a sentiment prediction result
>
> 2. The model returns a label (e.g. guilt) representing the predicted sentiment, which user can approve or revise
>
![png](assets/UC1b.png)
> 3. User clicks Approve button to accept the prediction result. The result is recorded to the DynamoDB
>
  ---
#### Scenario II
![png](assets/UC2a.png)
> 1. The RNN model prediction result returned does not quite met the user’s expectation. The user can click 1 of the 7 available label to override the returned result
>
![png](assets/UC2b.png)
> 2. User clicks ‘joy’ label to override the returned result ‘anger’. The revised result is recorded to the DynamoDB
>
 ---
#### Scenario III
![png](assets/UC3.png)
> User accesses the Csv file download endpoint to download prediction results stored in the DynamoDB. This csv file can then be used as a new dataset for retraining the RNN Sentiment Prediction model.
>
>
### Implementation Impediments and Resolutions
This is a POC (proof of concept) project the project team put together to implement and practice basic cloud DevOps concepts from this phase I Challenge and experiment advanced concepts nominated by team members.

The project was 100% unfunded and utilized AWS free-tier account to conduct the POC. The impediments experienced during the implementation and resolutions are listed below:

![png](assets/ImpRes.png)
