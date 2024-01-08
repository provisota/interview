# Scope
1. Authentication and Authorization:
    - Authentication is the process of verifying the identity of a user, device, or system. It often involves validating credentials like username and password. In Spring Security, you can use an `AuthenticationManager` to handle authentication.
    - Authorization is the process of granting or denying access to specific resources once the user is authenticated. It involves determining what an authenticated user is allowed to do. In Spring Security, you can use `AccessDecisionVoter` to handle authorization.

2. Access Control Models:
    - Discretionary Access Control (DAC): In this model, the owner of the resource decides who is allowed to access it. It's called "discretionary" because the control is based on the discretion of the owner.
    - Mandatory Access Control (MAC): In this model, access to resources is controlled by the system (not the owner), based on the levels of security assigned to each user and each resource.
    - Role-Based Access Control (RBAC): In this model, access to resources is based on the role of the user. Users are granted permissions based on their role, rather than their individual identity.
    - Attribute-Based Access Control (ABAC): In this model, access to resources is based on attributes associated with the user, the resource, the environment, and the action. It provides a high level of control and flexibility, but can be complex to implement.
# Questions
1. What is a difference between authentication and authorization?
2. What is a typical way to authenticate a user in REST API?
3. Can you name a few access control models (RBAC, ABAC, etc.) and describe differences between them?
# Answers
1. Authentication and Authorization:
    - Authentication is the process of verifying the identity of a user, device, or system. It often involves validating credentials like a username and password. It answers the question "Who is the user?".
    - Authorization, on the other hand, is the process of granting or denying access to specific resources once the user is authenticated. It involves determining what an authenticated user is allowed to do. It answers the question "What is the user allowed to do?".

2. In a REST API, a typical way to authenticate a user is by using tokens. The client sends their credentials (username and password) to the server. The server validates the credentials and sends back a token. The client can then use this token in the header of their requests to authenticate themselves. This is often done using the HTTP Authorization header with a type of Bearer.

3. Access Control Models:
    - Role-Based Access Control (RBAC): In this model, access to resources is based on the role of the user. Users are granted permissions based on their role, rather than their individual identity. For example, an "admin" role might have full access to every resource, while a "user" role might only have read access.
    - Attribute-Based Access Control (ABAC): In this model, access to resources is based on attributes associated with the user, the resource, the environment, and the action. It provides a high level of control and flexibility. For example, a rule might be "a user can view a document if the document is in the same department as the user and the document is not marked as confidential".
    - Discretionary Access Control (DAC): In this model, the owner of the resource decides who is allowed to access it. It's called "discretionary" because the control is based on the discretion of the owner.
    - Mandatory Access Control (MAC): In this model, access to resources is controlled by the system (not the owner), based on the levels of security assigned to each user and each resource. It is often used in environments that require a high level of security.