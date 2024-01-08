# CI/CD
Continuous Integration/Continuous Delivery (CI/CD) is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment.

1. **Value of CI/CD**:
    - **Faster release rate**: Automation in CI/CD enables teams to release software faster and more frequently.
    - **Reduced risks**: Regular integration and testing reduce the risk of finding late-stage lifecycle defects.
    - **Improved quality**: With CI/CD, you can ensure that every code change is reliable, maintainable, and of high quality.
    - **Better productivity**: CI/CD takes care of repetitive tasks, freeing up developers to focus on tasks that require a human touch.
    - **Faster feedback**: Any changes or improvements can be immediately tested and applied, leading to faster and more effective improvements.

2. **Main Principles of CI/CD**:
    - **Developers should merge their changes as often as possible**, at least once per day (Continuous Integration).
    - **Automate everything**: From integration, testing, to deployment, everything should be automated.
    - **Build quality in**: Instead of leaving testing to the end of the cycle, incorporate it from the beginning.
    - **Work in small batches**: Small updates are easier to troubleshoot and manage.
    - **Always be ready to release**: The master branch should always be in a deployable state.
    - **Build once, deploy anywhere**: The same build should be used across all environments.
    - **Observability**: Log, monitor, and trace everything for better visibility and quicker troubleshooting.
# Questions
1. What is (the purpose of) Continuous Integration (CI)?
2. What is (the purpose of) Continuous Delivery (CD)?
3. What are the main principle and pros/cons of CI?
4. What are the main principles and pros/cons of CD?
5. What are the CI/CD prerequisites?
6. You built it  you run it (describe principle, how to follow it)
7. Managing data(bases):
    * automated deployment and initialization
    * database scripting (schema migration)
    * managing datasets (test, production, etc).
8. Four key metrics (lead time, deployment frequency, mean time to restore, fail change percentage). What the show? When and why they can be useful?
9. Feature flags/toggles: pros/cons, toggle types (release, experiment, ops, permissions).
# Answers
1. Continuous Integration (CI) is a development practice where developers integrate code into a shared repository frequently, preferably several times a day. The purpose of CI is to catch integration issues early and reduce the time and effort required to release new software updates.

2. Continuous Delivery (CD) is a software development practice where code changes are automatically built, tested, and prepared for a release to production. The purpose of CD is to enable a constant flow of changes into production via an automated software production line.

3. The main principle of CI is to integrate early and often, so as to detect integration issues as soon as possible. Pros of CI include early detection of integration issues, reduced integration costs, and increased confidence in the software quality. Cons of CI include the need for a robust suite of tests, the need for a culture of frequent commits, and the need for a good CI system.

4. The main principles of CD are to keep the software deployable at any point and to build, test, and release incrementally. Pros of CD include reduced deployment risk, increased speed and frequency of delivery, and increased user satisfaction. Cons of CD include the need for a robust suite of tests, the need for a good CD system, and the need for close collaboration between various teams.

5. The CI/CD prerequisites include a version control system, automated build and test systems, a stable production environment, and a culture of collaboration and learning.

6. "You build it, you run it" is a principle that suggests that the team responsible for building a software component should also be responsible for running, monitoring, and troubleshooting it in production. This encourages developers to build more reliable and maintainable systems, as they are directly responsible for their operation.

7. Managing databases in a CI/CD context involves:
    - Automated deployment and initialization: Databases should be set up and initialized automatically as part of the deployment process.
    - Database scripting (schema migration): Changes to the database schema should be scripted and version-controlled, and these scripts should be run automatically during deployment.
    - Managing datasets: Different datasets (e.g., test, production) should be managed separately and should be loaded or migrated automatically as needed.

8. The four key metrics are:
    - Lead time: The time it takes for a change to go from code committed to code successfully running in production.
    - Deployment frequency: How often an organization successfully releases to production.
    - Mean time to restore (MTTR): The average time it takes to recover from a failure.
    - Change fail percentage: The percentage of changes to production that result in a failure.
      These metrics are useful because they provide a quantitative measure of the effectiveness of your CI/CD process and can help identify areas for improvement.

9. Feature flags/toggles are a technique for turning certain features of your application on or off at runtime. Pros include the ability to test features in production before they are complete, to perform A/B testing, and to enable or disable features without redeploying. Cons include added complexity and the potential for flags to become out of date or forgotten. Types of feature flags include:
    - Release toggles: Used to enable or disable features during the release process.
    - Experiment toggles: Used to perform A/B testing.
    - Ops toggles: Used to control operational aspects of the system’s behavior.
    - Permission toggles: Used to change the features or product experience that certain users receive.