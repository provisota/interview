# Serverless
1. **AWS Lambda Deployment**: AWS Lambda functions are deployed by creating a deployment package, which is a ZIP archive that contains your code and any dependencies. The deployment package is then uploaded to Lambda to create a new function version.

2. **AWS Lambda Limitations**: Some of the key limitations include:
    - Memory allocation ranges from 128 MB to 3008 MB.
    - Maximum execution time per request is 15 minutes.
    - Deployment package size is limited to 50 MB (zipped) and 250 MB (unzipped).
    - The number of file descriptors is 1024.
    - The number of processes and threads is 1024.

3. **AWS Lambda Retry Policies**: If a Lambda function fails, AWS Lambda will automatically retry the invocation twice, for a total of three invocations. However, if the function is invoked asynchronously and fails, you can configure the function to send invocation errors to a dead-letter queue (DLQ), which is an Amazon SQS queue or an Amazon SNS topic where the failed event is sent.

4. **Security**: AWS Lambda maintains compute resources in multiple isolated environments, and you can use Identity and Access Management (IAM) and Access Control Lists (ACLs) to assign granular access permissions to your Lambda functions. You can also configure your Lambda function to access resources inside your Virtual Private Cloud (VPC).

5. **Cold Start and Scaling**: A cold start occurs when you execute an inactive function for the first time. It includes the time it takes to load your function and run your initialization code. AWS Lambda automatically scales your applications in response to incoming request traffic. You can also enable Provisioned Concurrency to keep functions initialized and hyper-ready to respond in double-digit milliseconds.

6. **Execution Model**: When a Lambda function is invoked, AWS Lambda launches an execution context based on the configuration settings you provide. The execution context is a temporary runtime environment that initializes any external resources, such as database connections or HTTP endpoints, that your function needs to serve traffic.

7. **When to Use**: AWS Lambda is ideal for applications that need to respond quickly to new information or changes in the environment, need to process data in real-time, have variable workloads, or are composed of microservices or distributed systems. It's also a good choice when you want to focus on your application code, not on managing servers.
# Questions
1. How AWS Lambda is deployed and how it can be automated?
2. What frameworks can be used with AWS Lambda?
3. What  limitations do you know? (e.g. time)
4. How retries are working in AWS Lambda and what those do depend on?
5. Please list best practices to write lambda function
6. Security practices
7. What is cold start and how to deal with?
8. How AWS Lambda functions are executed and scaled?
9. What may affect AWS Lambda performance?
10. Please define pros and cons of going serverless and use cases when this will not work
# Answers
1. AWS Lambda functions are deployed by creating a deployment package, which is a ZIP archive that contains your code and any dependencies. The deployment package is then uploaded to Lambda to create a new function version. This process can be automated using AWS CLI, AWS SDKs, or infrastructure as code (IaC) tools like AWS CloudFormation or Terraform.

2. Several frameworks can be used with AWS Lambda to simplify the development and deployment of serverless applications. These include the Serverless Framework, AWS Serverless Application Model (SAM), and AWS Chalice (for Python), among others.

3. AWS Lambda has some limitations, such as a maximum execution time of 15 minutes per request, a deployment package size limit of 50 MB (zipped) or 250 MB (unzipped), and a /tmp directory storage limit of 512 MB.

4. AWS Lambda automatically retries failed function executions. For asynchronous invocation, AWS Lambda retries the function twice if the function returns an error. For stream-based event sources (e.g., Amazon Kinesis Data Streams, DynamoDB streams), AWS Lambda retries the records until the data expires.

5. Best practices for writing Lambda functions include keeping functions stateless, minimizing the deployment package size to its runtime necessities, using environment variables for configuration settings, setting appropriate function memory and timeout settings, and handling all paths in your function code (including exceptions).

6. Security practices for AWS Lambda include following the principle of least privilege when granting permissions, using environment variables to store sensitive information, and using AWS Identity and Access Management (IAM) roles to manage access to AWS resources.

7. A cold start in AWS Lambda is the initial execution of a function where AWS Lambda has to initialize a worker to run the function. To mitigate cold starts, you can use provisioned concurrency, which keeps functions initialized and ready to respond quickly.

8. AWS Lambda automatically scales your applications in response to incoming request traffic. You can also enable Provisioned Concurrency to keep functions initialized and hyper-ready to respond in double-digit milliseconds.

9. Factors that may affect AWS Lambda performance include the function's memory setting (which also affects CPU power and network capacity), the size of the deployment package, the runtime and function code, and the use of VPC.

10. Going serverless with AWS Lambda has several pros, such as no server management, automatic scaling, and cost-effectiveness as you only pay for the compute time you consume. However, it also has cons, such as the cold start issue, limitations of the platform (e.g., execution time, memory), and potential vendor lock-in. Use cases for serverless include microservices, real-time file processing, data transformation (ETL), and real-time stream processing. However, long-running applications, applications with complex dependencies, or applications requiring significant local file system storage may not be suitable for serverless.