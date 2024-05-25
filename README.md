# Blog Generator using AWS Bedrock and S3
This project contains an AWS Lambda function that generates a blog post on a given topic using AWS Bedrock and saves the generated content to an S3 bucket. The function leverages the Bedrock LLM model to create the blog content and Amazon S3 for storage.

## Features
Blog Generation: Generate a 200-word blog post on a specified topic using the Bedrock model.
S3 Integration: Save the generated blog post to an S3 bucket for persistent storage.
Error Handling: Handles errors gracefully and logs appropriate messages.

## Requirements
AWS Account
AWS Lambda
Amazon S3
AWS Bedrock
boto3 (AWS SDK for Python)
botocore


## Setup
AWS Configuration:

Ensure you have the necessary permissions to create and invoke Lambda functions, and access S3 and Bedrock services.
Create an S3 bucket to store the generated blog posts.

Environment Variables:

Set up your AWS credentials and default region in your environment or through AWS CLI configuration.

Lambda Deployment:

Package the Lambda function code and dependencies.
Deploy the package to AWS Lambda.

## Code Overview
blog_generate_using_bedrock(blogtopic: str) -> str
This function generates a blog post on the specified topic using the Bedrock model.

## Parameters:
blogtopic: The topic on which to generate the blog post.
Returns:
The generated blog post as a string.
save_blog_details_s3(s3_key: str, s3_bucket: str, generate_blog: str)
This function saves the generated blog post to the specified S3 bucket.

## Parameters:
s3_key: The S3 object key (path) where the blog post will be saved.
s3_bucket: The name of the S3 bucket.
generate_blog: The content of the blog post to save.

# lambda_handler(event, context)
The main Lambda handler function that processes incoming events.

## Parameters:
event: The event data passed to the Lambda function.
context: The runtime information of the Lambda function.

## Workflow:
Parses the incoming event to extract the blog topic.
Calls blog_generate_using_bedrock to generate the blog content.
Saves the generated blog post to S3 using save_blog_details_s3.
Returns a response indicating the completion of the blog generation process.

## Example Event Payload
``` json
{
  "body": "{\"blog_topic\": \"The future of AI in healthcare\"}"
}
```
## Deployment
Packaging the Lambda Function
Create a Deployment Package:

Package your Lambda function code along with its dependencies. You can use a tool like zip or AWS SAM to create the deployment package.
``` sh
zip -r lambda_function.zip lambda_function.py
```
Deploy the Lambda Function:

Upload the deployment package to AWS Lambda via the AWS Management Console, AWS CLI, or an infrastructure-as-code tool like AWS SAM or Terraform.

## Setting up AWS S3
Create an S3 Bucket:
Go to the S3 section of the AWS Management Console and create a new bucket to store the generated blog posts.

## Updating IAM Roles

Lambda Execution Role:
Ensure the Lambda execution role has the necessary permissions to access Bedrock and S3 services. Attach policies such as AmazonS3FullAccess and BedrockReadOnlyAccess (replace with the least privilege necessary for production).

## Testing
Invoke the Lambda Function:

You can test the function by invoking it through the AWS Management Console, AWS CLI, or by setting up an API Gateway trigger.
Check S3 Bucket:

After invocation, check the specified S3 bucket to ensure the blog post has been saved correctly.

## Troubleshooting
Permissions Issues: Ensure the Lambda execution role has the necessary permissions.
Timeouts: Adjust the Lambda function timeout settings if the Bedrock model invocation takes too long.
Error Logs: Check CloudWatch Logs for detailed error messages if the function fails.
