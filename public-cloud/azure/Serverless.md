# Serverless

## Azure Functions deployment
Azure Functions can be deployed using various methods such as Azure Portal, Azure CLI, Azure PowerShell, or directly from your IDE like Visual Studio or Visual Studio Code. You can also use Azure DevOps or GitHub Actions for CI/CD pipelines.

## Azure Functions limitations
Azure Functions do have some limitations such as the maximum execution time (which can be unlimited in the Consumption plan if you choose), memory size, and concurrent executions. The specific limitations depend on the hosting plan (Consumption, Premium, or Dedicated).

## Azure Functions types
Azure Functions support two types: In-Process (runs in the same process as the host) and Out-of-Process (runs in a separate process). The type depends on the runtime version and the language used.

## Azure Functions trigger types
Azure Functions support various trigger types such as HTTP, Timer, Blob Storage, Queue Storage, Event Hub, Service Bus, Cosmos DB, and more.

## Security model
Azure Functions use Azure Active Directory for authentication and can use role-based access control (RBAC) for authorization. You can also use function keys to secure the function at the function or HTTP trigger level.

## Cold start and scaling
Cold start is the initial delay when a function is invoked after being idle. This can be mitigated by using the Premium plan or keeping the function warm. Azure Functions can scale automatically based on the number of incoming events.

## Execution model
Azure Functions follow an event-driven execution model where each function is triggered by some kind of event like an HTTP request, a timer trigger, a message on a queue, etc.

## When to use
Azure Functions are best used when you have event-driven applications, you need to process data, integrate systems, work with IoT, build simple APIs or microservices, and when you want to focus on writing code and not managing infrastructure.

## Questions
1. How deploy a Azure Function?
2. What languages and frameworks supported?
3. What  limitations do you know? (e.g. time)
4. What retry policies Azure functions supports?
5. Please list best practicies to write Azure Functions?
6. List availlable triggers for the Azure functions?
7. What function types do you know?
8. When to use Durable functions?
9. What is Durable Orchestration? How to define Orchestration Identity?
10. What Function version exists? Difference between V1, V2? How to target different runtimes?
11. Security best practicies
12. What is cold start and how to deal with?
13. How to scale Azure functions?
14. When to use Azure Functions instead of WebJobs, Logic Apps, Power Automate
15. Please define pros and cons of going serverlesss and use cases when thiis will not work

## Answers
1. Azure Functions can be deployed using Azure Portal, Azure CLI, Azure PowerShell, directly from your IDE, or using CI/CD pipelines with Azure DevOps or GitHub Actions.
2. Azure Functions support several languages including C#, Java, JavaScript, TypeScript, Python, and PowerShell. The supported frameworks depend on the language used.
3. Some limitations of Azure Functions include maximum execution time, memory size, and concurrent executions. The specific limitations depend on the hosting plan.
4. Azure Functions support fixed-delay retries and exponential backoff delay retries.
5. Best practices for Azure Functions include keeping functions small and focused on a single task, using bindings to reduce boilerplate code, organizing functions into function apps based on scope and scalability, and setting appropriate retry policies.
6. Azure Functions support various triggers such as HTTP, Timer, Blob Storage, Queue Storage, Event Hub, Service Bus, Cosmos DB, and more.
7. Azure Functions support two types: In-Process and Out-of-Process.
8. Durable Functions should be used when you need to define stateful functions in a serverless environment, or when you need to chain functions together in a specific sequence.
9. Durable Orchestration is a way to define workflows in code by chaining together multiple functions. The Orchestration Identity is a unique identifier for running instances of the orchestration.
10. Azure Functions currently supports three major versions: V1, V2, and V3. V1 is the original runtime and only supports .NET Framework. V2 and V3 support .NET Core and additional languages. You can target a specific runtime by specifying the version in the function app settings.
11. Security best practices for Azure Functions include using Azure Active Directory for authentication, using RBAC for authorization, securing function keys, and using HTTPS for secure communication.
12. Cold start in Azure Functions is the initial delay when a function is invoked after being idle. This can be mitigated by using the Premium plan or keeping the function warm.
13. Azure Functions scale automatically based on the number of incoming events. You can also manually scale out function apps running on the Premium plan or a Dedicated (App Service) plan.
14. Azure Functions are best used for event-driven applications, while WebJobs are suitable for long running tasks, and Logic Apps and Power Automate are best for workflow-based integrations.
15. Going serverless with Azure Functions has several pros such as automatic scaling, pay-per-use pricing model, and reduced operational management. However, it also has cons like potential for cold start latency, stateless nature, and reliance on third-party providers. It might not be suitable for applications with complex infrastructure or specific compliance requirements.