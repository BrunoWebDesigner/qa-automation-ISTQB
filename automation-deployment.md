# Chapter 5: Implementation and Deployment Strategies for Test Automation

---

## 5.1 Integration to CI/CD Pipelines

### **5.1.1 Apply Test Automation at Different Test Levels within Pipelines**

**Key Points:**
- Test automation is best suited for CI/CD pipelines due to its ability to run unattended and provide rapid feedback.
- **Test levels in pipelines:**
  - **Configuration tests:** Run during the build of TAF/TAS to check file paths and script dependencies.
  - **Component tests:** Execute on individual components (e.g., library classes, API endpoints); serve as quality gates in CI.
      - *Career Example:* You ran API unit tests with each commit in GitHub Actions, blocking merges on failures.
  - **Component integration tests:** Run with component tests or as a separate step, testing interactions between components.
  - **System tests:** Usually run in the deployment phase (CD), validating the whole SUT after deployment.
      - *Career Example:* UI automation suites in Playwright executed post-deployment to preproduction.
  - **System integration tests:** Validate interactions between multiple systems, often in CD; catch issues between services or APIs.
- **Pipeline strategies:**
  - **Tests as deployment gates:** Failures trigger a rollback.
  - **Tests as post-deployment checks:** Failures require manual rollback; useful for nightly regression or exploratory runs.
- **Other usages:**
  - Scheduled nightly regression runs for longer suites.
  - Non-functional checks (e.g., performance) in dedicated pipelines.

---

### **5.1.2 Configuration Management for Testware**

**Key Points:**
- Configuration management is crucial for automation across multiple environments and SUT versions.
- **Elements to manage:**
  - **Test environment configuration:** URLs, credentials, feature toggles, etc. Store in config files or shared libraries.
      - *Career Example:* Used `config.json` and environment variables in Playwright/Cypress for different deployment stages.
  - **Test data:** Environment- or release-specific, externalized to CSV, JSON, or test data management systems.
      - *Career Example:* Test data for different clients stored in separate files for Postman collections.
  - **Test suites/cases:** Organized by purpose (smoke, regression, feature), mapped to pipelines, and grouped by tags.
      - *Career Example:* Playwright test suites for smoke, regression, and integration, triggered by pipeline tags.
- **Versioning:**
  - Use feature toggles to select appropriate tests for each release/environment.
  - Version testware alongside SUT releases using tags/branches to ensure compatibility.
      - *Career Example:* Tagged test automation releases to match deployed SUT versions in GitHub.

---

### **5.1.3 Test Automation Dependencies for an API Infrastructure**

**Key Points:**
- Understand **API connections** (how APIs interact and what business logic is exposed).
    - *Career Example:* Mapped Hub88 API dependencies to ensure tests didn’t break when a downstream service changed.
- **API documentation** (parameters, headers, sample payloads) is essential for building and maintaining automation.
    - *Career Example:* Generated tests from Swagger/OpenAPI docs for consistent coverage.
- **Contract testing:** Ensures that APIs interacting with each other adhere to agreed-upon behaviors and data formats.
    - **Consumer-driven:** Consumer specifies expectations.
    - **Provider-driven:** Provider specifies the contract.
    - *Career Example:* Considered using Pact for contract testing between Hub88 and third-party integrations.
- **Benefits of contract testing:**
    - Finds integration issues early.
    - Pinpoints which service is at fault.
    - Supports microservices and API-first systems.

---

## **Summary Table: Chapter 5 Topics & Career Examples**

| Topic                      | Key Points                                                         | Career Example                                       |
|----------------------------|--------------------------------------------------------------------|------------------------------------------------------|
| CI/CD Pipeline Integration | Run tests at config, component, integration, system levels          | GitHub Actions for API/UI tests, nightly regression   |
| Config Management          | Manage env config, test data, suites, versioning                   | config.json/env vars, tagged releases, Playwright     |
| API Dependencies           | Map API interactions, use docs, implement contract testing         | Swagger/OpenAPI-driven tests, Pact for integrations   |

---
**Use this chapter summary and examples to understand how to implement and manage test automation in CI/CD pipelines, maintain configuration, and handle dependencies for robust API testing.**