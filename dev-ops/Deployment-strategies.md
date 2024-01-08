# Deployment strategies
# Questions
1. What is zero downtime deployment and its pros/cons?
2. What is rolling deployment?
3. What is blue/green deployment?
4. What is canary deployment?
5. How to implement blue/green or canary no downtime deployment for a service with relational database (with schema or data migrations)?
# Answers
1. No Downtime Deployment: This is a deployment strategy that allows you to update your application without causing any disruption to the service. The benefits of this approach include improved availability and a better user experience, as users won't experience any service interruption during the deployment. However, implementing no downtime deployment can be complex, as it requires careful coordination and often additional infrastructure.

2. Rolling Deployment: In a rolling deployment, the application is deployed to a few nodes at a time, gradually replacing the old version with the new one. This approach minimizes the impact on resources and allows you to monitor the deployment process and abort it if something goes wrong. However, during the deployment, different versions of the application will be running simultaneously, which can cause compatibility issues.

3. Blue/Green Deployment: In a blue/green deployment, two environments (the "blue" and the "green") are maintained. The blue environment runs the current version of the application, while the new version is deployed to the green environment. Once the new version is tested and ready, the traffic is switched from blue to green. This approach allows for easy rollback in case of issues and ensures no downtime, but it requires double the infrastructure.

4. Canary Deployment: In a canary deployment, the new version of the application is gradually rolled out to a small subset of users before being rolled out to the entire infrastructure. This allows you to test the new version and monitor its performance and errors with a smaller impact. If the canary deployment is successful, the new version is gradually rolled out to all users. This approach reduces the risk of deploying a faulty version to all users at once, but it can be complex to implement and requires careful monitoring.