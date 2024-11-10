# CI/CD
## Important Links
- https://github.com/jenkinsci/docker
- 

## Continuous Integration and Continuous Deployment
- Continuous integration, delivery, and deployment (CI/CD) are foundational for successful DevOps practices.
- CI/CD focuses on building a streamlined, automated software release process.
- Teams practicing CI/CD gather continuous feedback by releasing software to the end user as quickly as possible, learning from users' experiences, and incorporating those insights into future releases.

## What is Continuous Integration ?
- Continuous Integration (CI) is a software development practice where developers frequently integrate code changes into a shared repository, ideally several times a day.
- Each integration is automatically verified by building the project and running a suite of automated tests.
- This process helps teams detect and address errors quickly, improve software quality, and reduce the time it takes to validate and release new software updates.

## Here's how CI typically works:
- **Frequent Code Commits:** Developers work on features or bug fixes in separate branches or forks.
  - When they're ready, they commit and push their changes to the central repository(Gitlab, github, gearit, bitbucket etc).
- **Automated Builds:**
  - A CI server (like Jenkins, GitHub Actions, GitLab CI, or CircleCI) detects the new code changes and automatically triggers a build process.
  - The server compiles the code, runs unit tests, and performs static code analysis, if configured.
- **Automated Testing:**
  - After the build, the CI server runs a set of automated tests, which may include unit tests, integration tests, and sometimes end-to-end tests.
  - This step ensures that recent changes do not introduce bugs or break existing functionality.
- **Feedback:**
  - If any part of the build or testing process fails, the CI system notifies the development team immediately, often through email, chat, or within the CI dashboard.
  - This rapid feedback loop enables developers to address issues while they're still small and fresh in mind.
- **Continuous Feedback & Monitoring:**
  - Even if the build succeeds, CI systems can provide reports on code quality, test coverage, and security vulnerabilities, helping teams improve code quality continuously.
## Benefits of CI
- **Early Bug Detection:**
  - CI helps identify bugs as soon as new code is integrated, reducing the time and cost associated with fixing them later in the process.
- **Improved Code Quality:**
  - Regular integration and automated testing improve overall code quality and reliability.
- **Faster Development Cycles:**
  - With CI, teams can work more efficiently, leading to shorter release cycles and faster feature delivery.
- **Reduced Integration Efforts:**
  - Instead of merging large code changes infrequently, small changes are integrated continuously, making code merges smoother and less risky.
  
## Popular CI Tools:
- Jenkins
- GitHub Actions
- Travis CI
- CircleCI
- GitLab CI
- Azure DevOps

# Continuous Deployment
- Continuous Deployment (CD) is an advanced software development practice where every code change that passes automated testing is automatically released to production.
- It extends the principles of Continuous Integration by not only integrating code changes frequently but also automating the entire release process, so new features, bug fixes, and updates are made available to users without manual intervention.
## How Continuous Deployment typically works:
- **Frequent Code Changes:**
  -  Developers push code changes to a shared repository, triggering Continuous Integration (CI) processes, which build the application and run automated tests (unit tests, integration tests, etc.).
- **Automated Testing and Validation:**
  - After the CI process, additional tests and validations may occur, such as performance tests, end-to-end tests, and security checks. Only if all tests pass does the change proceed to the next stage.
- **Automated Deployment to Production:**
  - Once validated, code changes are automatically deployed to production environments.
  - This deployment process is managed by a CD pipeline, which handles versioning, deployment strategies (such as blue-green deployment or canary releases), and rollback procedures if needed.
- **Monitoring and Feedback:**
  - After deployment, the application is monitored in production for issues or failures.
  - Monitoring systems provide real-time feedback on application performance, errors, and user experience. In case of any issues, automated rollback mechanisms may trigger, or alerts are sent to the development team.
## Benefits of Continuous Deployment
- **Rapid Feature Delivery:** New features, updates, and bug fixes reach end users quickly, creating a better user experience and keeping the product competitive.
- **Improved Feedback Loops:** Since every change is deployed immediately, developers receive rapid feedback from real user interactions, allowing them to iterate faster and improve features based on actual usage data.
- **Reduced Manual Intervention:** Automating deployments removes the need for manual release processes, which reduces human error and saves time.
- **Enhanced Developer Productivity:** Developers can focus on coding without worrying about deployment details, knowing their work will reach users automatically if it passes all automated checks.
## Difference Between Continuous Deployment and Continuous Delivery
- While similar, Continuous Deployment and Continuous Delivery are not the same:
- **Continuous Delivery:** Every code change is prepared for release and could be deployed to production, but the actual deployment may require a manual approval step.
- **Continuous Deployment:** Goes a step further by automating the deployment of every validated code change to production without manual approval, achieving full automation of the release process.
