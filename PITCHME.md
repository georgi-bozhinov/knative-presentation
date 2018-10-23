## Introduction to Knative

<img src="assets/knative-logo.png" width="200">

Georgi Bozhinov, SAP, 2018
---

### Knative is an open-source platform for deploying serverless workloads on K8S

---

- Provides a set of high-level key components that manage and automate the different aspects of deploying an application
- From source to url to the cloud, on premise or on a third-party data center.
- Functions, applications, containers

---

### Knative components

- Build - source-to-container build orchestration
- Eventing - management and delivery of events
- Serving - request-driven scaling, network programming, point-in-time snapshots of deployed code and configurations

---

### But first...

#### What is serverless?

- Run code without provisioning or managing servers
- The platform handles everything down to resource provisioning and managing processes
- Functions as a service (FaaS)
- Message-driven, microservice applications

---

### What is FaaS?

- Upload the code only, no application
- Functions act as microservices in the architecture of the application
- Run backend code without managing own server systems and long-lived apps
- Example: Responses to requests from client apps

---

### So how does Knative achieve this architecture?

---

### Knative components

* Build
