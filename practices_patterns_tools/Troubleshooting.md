# Troubleshooting
New Relic, DataDog, AirBrake, and Sentry are all popular tools for application performance monitoring (APM) and error tracking.  
New Relic: New Relic is a software analytics company that specializes in application performance management (APM). It provides real-time data that tracks the performance of your web applications and infrastructure. New Relic's tools monitor the performance and usage of your applications, the speed of your site, and the performance of your servers.  
DataDog: Datadog is a monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a SaaS-based data analytics platform. It provides a unified view across the entire stack from the frontend, backend, infrastructure, and cloud services.  
AirBrake/Sentry: Both Airbrake and Sentry provide real-time error tracking that gives you insight into production deployments. They collect and analyze errors in real-time, helping developers to build, deploy, and maintain quality software. They provide detailed exception reports that tell you what happened, what bit of code was involved, and allow you to recreate the error for debugging.  
These tools can be used to monitor application performance, track errors, and get detailed insights into production deployments. They can help you identify performance bottlenecks, track down errors, and understand how your applications are used in production.
# Questions
1. Which tools will you use (or suggest to use) to monitor production errors (tracebacks) both backend and frontend,
   in case if there are no centralized logging in place, and you need it ASAP?
2. Which tool will you use (or suggest to use) to monitor infrastructure, in case if you have limited time and need
   the result ASAP.
3. Which tool will you suggest to use in case if you need to set up performance monitoring of your system for both
   backend and frontend.
# Answers
1. To monitor production errors for both backend and frontend quickly, you can use error tracking tools like Sentry or Airbrake. These tools provide real-time error tracking that gives you insight into production deployments. They collect and analyze errors in real-time, helping developers to build, deploy, and maintain quality software. They provide detailed exception reports that tell you what happened, what bit of code was involved, and allow you to recreate the error for debugging.

2. To monitor infrastructure quickly, you can use a tool like Datadog or New Relic. Datadog is a monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a SaaS-based data analytics platform. New Relic, on the other hand, is a software analytics company that specializes in application performance management (APM). It provides real-time data that tracks the performance of your web applications and infrastructure.

3. For setting up performance monitoring of your system for both backend and frontend, you can use a tool like New Relic or Datadog. These tools provide comprehensive application performance monitoring features, including real user monitoring for frontend performance, server monitoring for backend performance, and distributed tracing for microservices performance.