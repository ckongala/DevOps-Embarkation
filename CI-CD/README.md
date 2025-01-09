
### **Continuous Integration (CI)**

1. **Build, Install Dependencies**:
   - **Maven (Java)** or **Gradle** for Java, **npm** or **Yarn** for Node.js, **pip** for Python, etc., are used to compile code and install dependencies.
   - **Example (Amazon, Uber)**: They use their respective build tools to create deployable artifacts and test dependencies before integrating code into the mainline.
   
2. **Dependency Check (OWASP Dependency-Check)**:
   - Automated security checks for known vulnerabilities in libraries used by the application (e.g., OWASP Dependency-Check).
   - **Example (Netflix)**: Automated dependency checks help prevent deploying code with outdated or insecure dependencies.

3. **Code Coverage & Unit Testing**:
   - Tools like **JUnit** (for Java), **Mocha/Chai** (for JavaScript), **pytest** (for Python) for running unit tests and ensuring code coverage.
   - **Example (Google)**: Google’s extensive unit tests and code coverage checks ensure the application runs as expected before proceeding further.

4. **Static Code Analysis (SonarQube/CodeQL)**:
   - Automated static code analysis tools like **SonarQube** or **CodeQL** analyze the source code for potential issues, including code smells and security vulnerabilities.
   - **Example (Uber)**: This is used to ensure the quality of codebase and maintainability across their microservices architecture.

5. **Dockerizing**:
   - Packaging the application into a **Docker** container for consistent environment setup across all stages (development, testing, production).
   - **Example (Netflix)**: Docker ensures Netflix's services can run across different environments without compatibility issues.

6. **Vulnerability Scan (Snyk, Trivy, or Aqua Security)**:
   - Tools like **Snyk**, **Trivy**, or **Aqua** are used to scan container images for vulnerabilities in the base images or dependencies.
   - **Example (TikTok)**: They perform vulnerability scanning to ensure that the containers are secure before deployment.

7. **Push Image to Container Registry (ECR, Docker Hub)**:
   - Once the Docker image is created and tested, it's pushed to a **Container Registry** like **Amazon ECR**, **Google Container Registry**, or **Docker Hub**.
   - **Example (Amazon)**: ECR provides an easily accessible container registry for Amazon services to pull from.

---

### **Continuous Deployment (CD)**

1. **Run Image in AWS EC2 (or other infrastructure)**:
   - **EC2** instances (or alternatives like **Google Cloud Compute Engine**, **Azure VM**) are used to host and run the Docker container image.
   - **Example (Amazon)**: AWS EC2 instances are the primary compute infrastructure for deploying applications in Amazon’s microservices environment.

2. **Integration Testing**:
   - Running integration tests to ensure that different components work together properly after deploying the code in the containerized environment.
   - **Example (Uber)**: They perform integration tests after deploying the code to ensure that the various microservices interact correctly.

---

### **Continuous Delivery (CD)**

When a **pull request** is raised, the **Continuous Delivery** pipeline kicks in:

1. **Deploy to Kubernetes (k8s) with GitOps-ArgoCD**:
   - **ArgoCD** is a GitOps-based deployment tool for Kubernetes. Developers update Docker image tags, and ArgoCD automatically deploys the latest images to the Kubernetes cluster.
   - **Example (Google)**: Google uses Kubernetes for its scalability, and **GitOps** ensures that deployments are automatically synced to the desired state in Kubernetes.

2. **DAST (OWASP ZAP - Dynamic Application Security Testing)**:
   - **OWASP ZAP** is a tool used for dynamic security testing of web applications to find vulnerabilities while running in a real-world environment.
   - **Example (Netflix)**: Netflix uses automated DAST scans to test for runtime security vulnerabilities in their application as part of their CI/CD pipeline.

3. **Approval Stage (Manual Approval)**:
   - Before going to production, a manual approval process might be set up, requiring a reviewer to check the code, tests, and security findings.
   - **Example (Amazon)**: Amazon’s security and compliance teams often have the final say on whether a change should go live, ensuring no unintended vulnerabilities are introduced.

4. **AWS Lambda (Update Configurations for Serverless)**:
   - **AWS Lambda** is used for serverless functions that might handle configuration updates or other dynamic processes. It enables flexible updates without managing servers.
   - **Example (Uber)**: Uber uses **AWS Lambda** for backend automation tasks, serverless microservices, and configuration changes.

5. **Lambda Invocations/Testing**:
   - Testing Lambda invocations as part of the deployment process to ensure that serverless functions work as expected.
   - **Example (TikTok)**: TikTok leverages serverless architectures to run short, event-driven tasks that scale efficiently.

---

### **Post-Build Reports** (for monitoring & validation)

1. **Unit Test Reports**:
   - Detailed reports on unit tests that show which tests passed, which failed, and overall test coverage.
   - **Example (Google)**: Google relies heavily on unit test reports to ensure that all internal code behaves as expected.

2. **Code Coverage Reports**:
   - Code coverage is analyzed to ensure a good percentage of the codebase is tested.
   - **Example (Netflix)**: Netflix uses these reports to ensure the robustness of their application and minimize defects in production.

3. **Vulnerability Reports**:
   - Automated reports generated by security tools like **OWASP**, **Snyk**, or **Trivy** to inform about any potential vulnerabilities in the application or infrastructure.
   - **Example (Amazon)**: Amazon checks these reports in its security-focused CI/CD pipeline to maintain a secure deployment process.

4. **Dependency Scan Reports**:
   - Scans for outdated or vulnerable dependencies that could impact security or stability.
   - **Example (Uber)**: Uber regularly scans their dependencies to minimize security risks and technical debt.

5. **Publish Reports to Jenkins, S3 & Slack Notifications**:
   - All the reports (Unit Test, Coverage, Vulnerabilities) are published to **Jenkins** for CI/CD visibility, stored in **S3** for archival, and pushed to **Slack** for real-time notifications to the development team.
   - **Example (Netflix)**: Slack notifications keep Netflix’s engineering teams informed on the build status, test results, and deployment outcomes.

---

### Final Summary
Real-world companies like Amazon, Google, Netflix, Uber, and TikTok implement CI/CD pipelines that focus on automating code integration, security, testing, and deployments at scale. These companies prioritize **automation** and **security** at each stage of the pipeline, making sure their services are always secure, scalable, and efficient across multiple environments.

