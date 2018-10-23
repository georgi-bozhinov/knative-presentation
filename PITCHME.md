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

---

### Build

* A build is a resource in Knative to fetch, build and package code on-cluster.
* Defined in a single config file
* Build templates ( Kaniko, cf buildpack template ) - reusable build pipelines
* Example: Fetch code from github, use docker image to build it and deploy it on-cluster

---

### Build

```
spec:
  source:
    git:
      url: https://github.com/knative/build.git
      revision: master
  steps:
  - image: ubuntu
    args: ["cat", "README.md"]
  steps:
  - Read secrets, deploy other images...
```

---

### Knative components

* Serving

---

### Serving

Builds on K8S and Istio to support deploying and serving of serverless apps and functions

---

### Serving

Features:

* Rapid deployment of serverless containers
* Autoscaling up and down
* Network programming - routing, ingress, services, load balancing for distributed microservices
* Point-in-time snapshots of deployed code ( called Revisions )

---

### Serving - Service

* Knative serving gives us a Service abstraction
* Not to be confused with all the other meanings of service in this context
* Manages lifecycle of the workload. Creates objects to ensure app has route, a configuration and a new revision on each update.

---

### Serving - Route

* Maps a network endpoint to one of more revisions.

---

### Serving - Configuration

* Maintains the desired state for the deployment. Modifying it creates a new revision.

---

### Serving - Revision

* Point-in-time snapshot of the code. Linear history for each new modification. Revisions are immutable.

---

### Build + Serving

An end-to-end deployment from source

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: app-from-source
  namespace: default
spec:
  runLatest:
    configuration:
      build:
        serviceAccountName: build-bot
        source:
          git:
            url: https://github.com/mchmarny/simple-app.git
            revision: master
        template:
          name: kaniko
          arguments:
          - name: IMAGE
            value: docker.io/{DOCKER_USERNAME}/app-from-source:latest
      revisionTemplate:
        spec:
          container:
            image: docker.io/{DOCKER_USERNAME}/app-from-source:latest 
            imagePullPolicy: Always
            env:
            - name: SIMPLE_MSG
              value: "Hello sample app!"
```

---
