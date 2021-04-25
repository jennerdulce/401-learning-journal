# API Gateway, Lambda, DynamoDB

## Overview

- Walk through on all the things needed to build out a AWS Serverless API (API Gateway) along with Serverless Functions (lambda) that retrieves, stores, and manipulates data from a AWS DynamoDB database

## IAM

- Head into the **Roles** tab on the right
  - The Roles grant permissions which are needed to utilize AWS tools
  - i.e. if you want to use CLOUD WATCH which is a logger for your lambda functions, you will need to make a role that has this type of permission which will later be tied to the API Gateway along with the lambda function
- Create Role Lambda
- Permissions
  - DynamoDBFullAccess
  - AWSLambda_FullAccess
  - CloudWatchFullAcces
- Enter Role Name
  - Create the role

## Lambda

- Create function
- Choose a relevant variable name on what this function will do
- Permissions
  - Use existing role that you created
  - Creates the function with all access to DynamoDB, Lambda, And Cloudwatch
  - within the lambda function, `console.log(event)`
    - Allows you to see event object passed in while utilizing Cloudwatch Logs

## DynamoDB

- Create table
- tablename
  - primary key
    - make key = id
  - THIS MUST MATCH THE TABLE NAME IN THE SCHEMA OF YOUR DYNAMOOSE SCHEMA FILE

## API Gateway

- Create API
- HTTP API
- Integrations
  - Lambda
  - Choose correct Lamba function
- API Name
- Choose correct method that correlates to what your lambda function does
- Stage Name
  - Default
- Create

### CORS

- All origins
- All methods
- All headers

## Deployment Package

- npm init -y
- npm i dynamoose
- `schema.js`
- `index.js`
  - Be sure that this file name `index` matches the handler name when you create a lambda function
  - `index.js` file should contain the structure of a lambda function
  - in this example we added code that interacts with a AWS DynamoDB `clients`
- `zip -rp functionname.zip *`
  - wraps all the contents within a zip file
  - this zip file is then used to 'upload from zip' on the Lambda > code page

### YML File

- Go in github create yml file

```yml
# CHANGE
name: aws-get  

on:
  push:
  # CHANGE
    branches:
      - main

jobs:
  deploy_source:
  # CHANGE
    name: build and deploy lambda
    strategy:
      matrix:
        node-version: [12.x]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - name: Install dependencies
        run: npm install
      - name: Zip Functions
        run: |
          zip -rp function.zip *
      - name: deploy content to aws lambda
        uses: appleboy/lambda-action@master
        with:
        # CHANGE
          aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws_region: ${{ secrets.AWS_REGION }}
          function_name: get-jdd
          zip_file: ./function.zip
```

## TIPS

- refer to DynamoDB Lab

### Flow for testing

- Edit file
- Delete old zipped file
- create new zip file
  - `zip -rp functionname.zip *`
- Go on AWS > Lambda > Upload from Zip
- Run a test or use an API Testing tool such as Swagger, Postman, Insomnia

## Problems I came across

- The `event.body` needs to be parsed
- Sending back information through the response Body needs to be `JSON.tringify()`
- Console.log the event
- There was an issue the cloud watch said it did not have permissions to read the file
  - Solution: `chmod -R 644 index.js ` when creating the initial file, be sure to to type this code for the index as well as any other file to grant read access
