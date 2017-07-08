# Amazon Web Service (AWS) 

AWS

## Compute Services

### Lambda

AWS Lambda allows you to run your own code in response to events in a serverless enviroment.

**Serverless Computing**

Serverless is a type of event-driven architecture functions are reacting to specific type of trigger events. Minimizing the need for IT infrastructure. Speaking of AWS, it can be an event fired by S3, SNS or the API Gateway just to name a few. Means that you can run your own code without provisioning and managing your computer resource.

Before create a Lambda function or used Serverless Frameworks for manages your function application code and infrastructure, we need first to give it access keys for your AWS account.

Preparation:

1. Log in or sign up for a new AWS account.
2. Navigate to the Identity & Access Management (IAM) service and create a new Group called `serverless-group`. On the left sidebar of the Identity & Access Management (IAM) area, click on **Groups** and them **Create New Group**. Add the name `serverless-group`, and then click **Next Step** and on Attach Policy we are going to attach to this group **AdministratorAccess** checking his checkbox them click **Next Step**, review all the details of the group and click **Create Group**.
3. Navigate to the Identity & Access Management (IAM) service and create a new User called `serverless-admin`. On the left sidebar of the Identity & Access Management (IAM) area, click on **Users** and them **Add user**. Add the name `serverless-group`, then check on the checkbox **Programmatic access** to allow development and click **Next: Permissions**. On set permissions area check the group `serverless-group` and click **Next: Review**. After review all details, click **Create user**.
4. After create the user, AWS provide you a table with the **user**, **access key id** and **secret access key**. Copy all items and saved on a secure document for future used.

**Lambda and API Gateway**

Exercise 1: Simple "Hello from Lambda"

1. Navigate to the Lambda service.
2. If you don't have any previous Lambda function you go ahead and click **Get Started Now** otherwise click on **Create a Lambda function**.
3. On Select bluprint, Amazon Web Service will offer you a list of functions code template with some dummi code. On this case we are going to select as runtime **Node.js 4.3** and **Blank Function**.
4. Now we need to configure triggres, Amazon Web Service give us many triggers options but for this case we are going to leave this empty and click **Next**.
5. On configuration of the function we can strat we adding the name of the function. `firstLambda`, add description and runtime. Then we can see the Lambda code:

```javascript
exports.handler = (event, context, callback) => {
  callback(null, 'Hello from Lambda');
};
```

* **event** - This variable is used by Lambda to pass in event data to the handler (like an HTTP request).
* **context** - The context variable is used to pass in runtime information for the Lambda function, like how much time is remaining before the function will be terminated.
* **callback** - By using it, you can explicitly return data to the caller (like an HTTP response).

6. Moving to Lambda function handler and role, click on dropdown **Role** and click on **Create a custom role**. Create a new (IAM) Role, with `lambda_basic_execution` and click **Allow**.
7. Then click on dropdown **Advanced settings**, we can add memory on this section, remember if you add more memory and as more memory more higher payment, so for this case we can leave as default `128`. Now we can click **Next**.
8. Review all details of your Lambda and click **Create function**.
9. After successfully creation you can test your function by clicking on the **Test** button on the upper area. After test you will see:

```
"Hello from Lambda"
```

10. Now for Adding API Gateway, Navigate to the API Gateway service. If you don't have any previous API Gateway you go ahead and click **Get Started** otherwise click on **Create API**.
11. On Create new API, we check on radio selector **Example API**, then click on **Import**. Now will see our example API.
12. Click on **APIs** on the left sidebar of the API Gateway area and then click on **Create API**.
13. Add name of your API, on this case `firstAPI` and click **Create API**.
14. To configured you API click on dropdown **Action -> Create Resource**. Add a name for this resource, on this case `foo` and click **Create Resource**.
15. On selection the previous resources we can add a method, by clicking on dropdown **Action -> Create Method** and then on the dropdown under resource select `GET` and click the success icon.
16. Now we can integrate Lambda function. On this case on `GET` method setup check on **Integration type** select `Lambda Function` then on **Lambda Region** select your region and then type the name of the function you want to integrate. On this case `firstLambda`. And click **Seve**.
17. After sucessfully integration, click on **TEST** for testing purpose. Will see the return value:

```
"Hello from Lambda"
```

**Serverless Framework**

The Serverless framework is an open-source, MIT-licensed solution which helps with creating and managing AWS Lambda functions easier.

1. First install Nodejs on machine. Ensure that you have installed latest LTS version of Nodejs. 
2. Install by terminal Serverless as global:

```
npm install -g serverless
```

3. To see options after install type on terminal:

```
serverless
```

4. Create new project directory for our serverless service, then place your terminal on the new directory. Now to create the project type on terminal:

```
serverless create --template aws-nodejs --name simpleLambda
```

or

```
sls create -t aws-nodejs -n simpleLambda
```

5. Our previous terminal command, create a serverless project by choosing **AWS Nodejs** template and adding the name `simpleLambda`. When creating a new service is finished, we will see file structure in the project folder: 

* **serverless.yml** - a YAML file where we will define configurations for our service, such as AWS Resources (S3, DynamoDB, etc), Region, Nodejs Runtime, we want to use and also our service’s functions configurations.
* **handler.js** - Initial Javascript file , created by serverless, that is supposed to be the place where we will write our function’s logic. 

```javascript
'use strict';

module.exports.hello = (event, context, callback) => {
  const response = {
    statusCode: 200,
    body: JSON.stringify({
      message: 'Go Serverless v1.0! Your function executed successfully!',
      input: event,
    }),
  };
  
  callback(null, response);
};
```

* **.gitignore**

6. Open the **serverless.yml** file and edit these Configuration sections: `handler`. This section route to your **handler.js** file function.

```
functions:
  hello:
    handler: handler.hello
```

7. To deploy our function to AWS first we need to configurated our serverless framework on our machine with ours AWS credential.

* To setup credential on serverless, by terminal type:

```
serverless config credentials --provider aws --key xxx --secret yyy
```

* In case we already have a previous olds credentials we can remove that old credentials by following this steps on terminal:

```
cd ~
cd .aws
rm credentials
```

8. Let deploy our services to AWS:

```
serverless deploy --function simpleLambda
```

* Note: After deploy, AWS will provide the following details:

```
Service Information
service: simpleLambda
stage: dev
region: us-east-1
api keys:
  None
endpoints:
  None
functions:
  hello: simpleLambda-dev-hello
```


9. To test our service we need to invoke our function, remember our function is `hello`, not the name of the services:

```
serverless invoke -f hello
```

* Response

```json
{
  "statusCode": 200,
  "body": "{\"message\":\"Go Serverless v1.0! Your function executed successfully!\",\"input\":{}}"
}

```

10. To test our function on local and not on AWS we can type:

```
serverless invoke local -f hello
```

11. Let add method name associated to HTTP path and verbs. We need to add to our **serverless.yml** the following:

```
functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: hello
          method: get 
```

12. After deploy, AWS provide the url to test on browser.

```
Service Information
service: simpleLambda
stage: dev
region: us-east-1
api keys:
  None
endpoints:
  GET - https://jn1lnbbj9k.execute-api.us-east-1.amazonaws.com/dev/hello
functions:
  hello: simpleLambda-dev-hello
```