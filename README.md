Introduction



As a DevOps learner, one of the biggest gaps I noticed was between knowing individual tools and connecting them into a real workflow.

This project was built to close that gap.



The goal was simple on paper:



Deploy a Hello World Go application using a fully automated CI/CD pipeline.



The execution, however, required solving real-world DevOps challenges involving Jenkins, Docker, GitHub, and Kubernetes — especially while working on Windows and running Jenkins inside Docker.

Problem Statement



Most beginner projects:



* Stop at building an app



* Or deploy manually to Kubernetes



* Or skip CI/CD altogether



In real production environments:



* Code changes must automatically trigger builds



* Images must be securely pushed to a registry



* Deployments must be repeatable and reliable



This project focuses on automation, reproducibility, and correctness, not application complexity.



Project Objectives



* Build a lightweight Go web application



* Containerize it using Docker best practices



* Automate build and deployment using Jenkins



* Deploy and load-balance the application on Kubernetes



* Handle real DevOps issues instead of idealized setups



High-Level Architecture

Local Development (Windows CMD)

&nbsp;       ↓

&nbsp;     GitHub

&nbsp;       ↓

&nbsp;Jenkins (Running in Docker)

&nbsp;       ↓

&nbsp;Docker Image Build

&nbsp;       ↓

&nbsp;Docker Hub Registry

&nbsp;       ↓

&nbsp;Kubernetes Deployment

&nbsp;       ↓

&nbsp;Load Balanced Service



Application Design



The application is a simple Go HTTP server:



* Listens on port 8080



* Responds with a static message



* Designed to be stateless and container-friendly



This keeps the focus on infrastructure and automation, not application logic.



Containerization Strategy



A multi-stage Docker build was used to:



* Compile the Go binary in a builder image



* Run it inside a minimal Alpine image



* Reduce image size and attack surface



This mirrors how production-grade containers are built.



CI/CD with Jenkins (Inside Docker)



Jenkins was intentionally run inside a Docker container to simulate real-world isolation.



Key Challenges Faced



* Jenkins container did not have Docker CLI installed



* Docker socket access was required to build images



* Branch mismatch (main vs master) caused pipeline failures



* Duplicate SCM checkout caused unexpected behavior



Solutions Implemented



* Installed Docker CLI inside Jenkins container



* Mounted Docker socket to Jenkins container



* Standardized Git branch usage



* Removed redundant checkout stages from Jenkinsfile



Secure Image Push with Docker Hub



Instead of hardcoding credentials:



* A Docker Hub access token was generated



* Credentials were stored securely in Jenkins



* Jenkins Credentials ID was used inside the pipeline



This follows CI/CD security best practices.



Kubernetes Deployment



The application was deployed to a local Kubernetes cluster using Docker Desktop.



Deployment Features



* Multiple replicas for high availability



* Load-balanced service



* Declarative YAML configuration



Zero-downtime redeployments on pipeline reruns



Results



* Any GitHub push triggers Jenkins automatically



* Docker image is rebuilt and pushed



* Kubernetes deployment is updated



* Application remains accessible through a load-balanced endpoint



The pipeline now behaves like a real production CI/CD workflow.



Key Learnings



* CI/CD failures often come from environment assumptions



* Jenkins inside Docker requires explicit tooling setup



* Branch consistency is critical in Git-based pipelines



* Automation exposes issues manual workflows hide



* Debugging CI logs is a core DevOps skill



Why This Project Matters



* This project demonstrates:



* Tool integration, not isolated knowledge



* Problem-solving over tutorial copying



* Understanding of real CI/CD constraints



It is intentionally simple in scope but deep in execution.



Future Improvements



* GitHub webhooks for event-based triggering



* Jenkins deployed on Kubernetes



* Helm-based deployments



* Ingress with NGINX



* Monitoring with Prometheus and Grafana



Conclusion



This project helped bridge the gap between learning DevOps tools and using them the way they’re used in real systems.



It reinforced an important lesson:



Automation doesn’t just save time — it exposes reality.

