
# Jenkins Shared Library — RoboShop CI/CD
 
Reusable Jenkins pipeline library for RoboShop microservices.
Write pipeline logic once — reuse across all microservices.
 
---
 
## Why Shared Library
 
Without Shared Library:
- 10+ microservices × 1 Jenkinsfile each = many files to maintain
- One change (e.g. Trivy severity) = update every Jenkinsfile
 
With Shared Library:
- One pipeline definition in this repo
- Each microservice Jenkinsfile calls it in 3 lines
- One change propagates to all services automatically
 
---
 
## Structure
 
```
jenkins-shared-library/
└── vars/
    └── deployPipeline.groovy    # Node.js EKS pipeline
    └── nodeJSEKSPipeline.groovy # Reusable pipeline function
```
 
---
 
## How to Register in Jenkins
 
```
Manage Jenkins → System → Global Pipeline Libraries
 
Name:            jenkins-shared-library
Default version: main
Retrieval:       Modern SCM → Git
URL:             https://github.com/mamatha-ravi/jenkins-shared-library
```
 
---
 
## How to Use in Jenkinsfile
 
Each microservice needs only a few lines:
 
```groovy
@Library('jenkins-shared-library') _
 
def configMap = [
  project:   "roboshop",
  component: "catalogue"
]
 
nodeJSEKSPipeline(configMap)
```
 
---
 
## Pipeline Stages
 
```
Code Push to GitHub
      ↓
Jenkins triggers automatically
      ↓
Install dependencies — npm install
      ↓
Run unit tests
      ↓
SonarQube code quality scan
      ↓
Docker build and tag
      ↓
Trivy security scan (CRITICAL fails build)
      ↓
Push to AWS ECR
      ↓
Helm upgrade --install (deploy to EKS)
      ↓
Verify rollout status
```
 
---
 
## Key Features
 
- **Shared logic** — all microservices use same pipeline stages
- **Trivy gate** — CRITICAL CVE blocks deployment automatically
- **SonarQube integration** — code quality enforced on every PR
- **ECR push** — automatic AWS authentication before image push
- **Helm deploy** — deploys to Kubernetes EKS with --atomic flag
 
---
 
## Tech Stack
 
Jenkins · Groovy · Docker · AWS ECR · Helm · Kubernetes · Trivy · SonarQube
 
---
 
## Related Repos
 
| Repo | Description |
|------|-------------|
| [terraform-aws-eks](https://github.com/mamatha-ravi/terraform-aws-eks) | EKS cluster this pipeline deploys to |
| [catalogue-unit-tests](https://github.com/mamatha-ravi/catalogue-unit-tests) | Example service using this library |
 
---
 
## Author
 
Mamatha Ravipati
📍 Hyderabad, India
📧 mamata.r@gmail.com
🔗 [github.com/mamatha-ravi](https://github.com/mamatha-ravi)


