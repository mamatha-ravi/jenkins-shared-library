
# RoboShop Infrastructure — AWS DevOps Project
 
Complete production-equivalent DevOps infrastructure for RoboShop
microservices e-commerce application built as a personal learning project.
 
## Architecture
 
```
Internet → Route 53 → ALB → EKS Nodes → RDS
                      ↓
              VPC (Public + Private Subnets)
              3 Availability Zones
```
 
## What is Included
 
| Component | Technology |
|-----------|------------|
| Cloud Infrastructure | AWS (VPC, EKS, RDS, ALB, Route 53, ECR) |
| Infrastructure as Code | Terraform |
| Container Orchestration | Kubernetes + Helm |
| CI/CD Pipeline | Jenkins + Shared Library |
| Configuration Management | Ansible |
| Monitoring | Prometheus + Grafana + Alertmanager |
| Security Scanning | Trivy |
| Container Registry | AWS ECR |
 
## Infrastructure Setup
 
### 1. VPC and Networking
- Custom VPC with public and private subnets
- 3 Availability Zones for high availability
- NAT Gateway for private subnet internet access
- Internet Gateway for public subnet
 
### 2. EKS Cluster
- Managed node groups with auto-scaling
- IRSA (IAM Roles for Service Accounts)
- AWS Load Balancer Controller
- TargetGroupBinding for direct pod IP routing
 
### 3. Kubernetes Deployments
- Resource requests and limits on all pods
- Liveness, Readiness, and Startup probes
- HorizontalPodAutoscaler (HPA)
- PodDisruptionBudget (PDB)
- TopologySpreadConstraints across AZs
 
### 4. CI/CD Pipeline
- Jenkins Shared Library for reusable pipelines
- Docker multi-stage builds
- Trivy security scanning
- ECR image push with version tags
- Helm deploy with --atomic rollback
 
### 5. Monitoring
- Prometheus via kube-prometheus-stack
- Grafana dashboards for RED metrics
- Alertmanager routing to Slack
- ServiceMonitor for each microservice
 
## Tech Stack
Terraform · Kubernetes · Helm · Jenkins · Docker · Ansible ·
Prometheus · Grafana · AWS EKS · AWS RDS · AWS ALB · AWS ECR
