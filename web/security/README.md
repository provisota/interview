# Scope
1. Injection and OWASP Top 10:
    - Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. The attacker's hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.
    - The OWASP Top 10 is a standard awareness document for developers and web application security. It represents a broad consensus about the most critical security risks to web applications. The top 10 vulnerabilities are Injection, Broken Authentication, Sensitive Data Exposure, XML External Entities (XXE), Broken Access Control, Security Misconfigurations, Cross-Site Scripting (XSS), Insecure Deserialization, Using Components with Known Vulnerabilities, and Insufficient Logging & Monitoring.

2. XSS (Cross-Site Scripting) and CSRF (Cross-Site Request Forgery):
    - XSS flaws occur whenever an application includes untrusted data in a new web page without proper validation or escaping, or updates an existing web page with user-supplied data using a browser API that can create HTML or JavaScript. XSS allows attackers to execute scripts in the victim's browser which can hijack user sessions, deface web sites, or redirect the user to malicious sites.
    - CSRF is an attack that tricks the victim into submitting a malicious request. It uses the identity and privileges of the victim to perform an undesired function on their behalf. For most sites, browser requests automatically include any credentials associated with the site, such as the user's session cookie, IP address, etc. Therefore, if the user is authenticated to the site, the site cannot distinguish between legitimate requests and forged requests.
# Questions
1. What is OWASP top 10 and what vulnerabilities you know?
2. For any vulnerability how to prevent?
3. What is XSS and how to prevent it?
4. What is CSRF & when it is applicable?
# Answers
1. The OWASP Top 10 is a standard awareness document for developers and web application security. It represents a broad consensus about the most critical security risks to web applications. The top 10 vulnerabilities are Injection, Broken Authentication, Sensitive Data Exposure, XML External Entities (XXE), Broken Access Control, Security Misconfigurations, Cross-Site Scripting (XSS), Insecure Deserialization, Using Components with Known Vulnerabilities, and Insufficient Logging & Monitoring.

2. Prevention of these vulnerabilities often involves secure coding practices and using security frameworks that protect against such issues. For example, to prevent injection flaws, you should use a safe API which avoids the use of the interpreter entirely or provides a parameterized interface. To prevent broken authentication, you should implement multi-factor authentication that isn't reliant on weak credentials.

3. Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user. To prevent XSS, you should escape untrusted HTTP request data based on the HTML context (body, attribute, JavaScript, CSS, or URL) that the data will be placed into.

4. Cross-Site Request Forgery (CSRF) is an attack that tricks the victim into submitting a malicious request. It uses the identity and privileges of the victim to perform an undesired function on their behalf. CSRF is applicable when a malicious web site, email, blog, instant message, or program causes a user's web browser to perform an unwanted action on a trusted site for which the user is currently authenticated. To prevent CSRF attacks, you should use anti-CSRF tokens and same-site cookies.