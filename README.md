# Ascii Artify

#####Програмний продукт для перетворення зображень у ascii-art за допомогою Machine Learning

![Image](.data/demo.gif)


Ascii Artify can be deployed on:

| Platform  | Description  | Pros  | Cons | Supported OS | Monitoring | Scaling | Supported Architecture | Automation |
|-----------|--------------|-------|------|--------------|------------|---------|------------------------|--------------------------|
| [**Minikube**](https://kubernetes.io/docs/tutorials/hello-minikube/) | A lightweight Kubernetes implementation designed for local development and testing.  | - Supports multiple hypervisors, including VirtualBox and Hyper-V. <br> - Easy to set up and use. <br> - Good for testing Kubernetes functionality locally.  | - Not suitable for large-scale production environments. <br> - Limited performance compared to full Kubernetes clusters. <br> - May require manual configuration for some features. | Linux, macOS, Windows | Prometheus, Grafana, ELK Stack | Horizontal Pod Autoscaler | x86-64, ARM64 | Ansible, Terraform, Helm |
| [**Kind**](https://kind.sigs.k8s.io) | A tool for running local Kubernetes clusters using Docker containers as nodes.  | - Can be used with any Docker-compatible runtime, including Docker Desktop. <br> - Supports multiple nodes for more complex environments. <br> - Good for testing Kubernetes functionality locally.  | - Limited performance compared to full Kubernetes clusters. <br> - May require manual configuration for some features. <br> - Requires some knowledge of Docker and Kubernetes. | Linux, macOS, Windows | Prometheus, Grafana, ELK Stack | Horizontal Pod Autoscaler | x86-64, ARM64 | Ansible, Terraform, Helm |
| [**k3d**](https://k3d.io/v5.4.9/#installation)  | A lightweight Kubernetes distribution designed for local development and testing.  | - Fast and easy to set up and use. <br> - Supports multiple Kubernetes versions. <br> - Good for testing Kubernetes functionality locally.  | - Limited performance compared to full Kubernetes clusters. <br> - May require manual configuration for some features. <br> - Not as widely used as Minikube or Kind. | Linux, macOS | Prometheus, Grafana | Horizontal Pod Autoscaler | x86-64 | Ansible, Terraform, Helm |

###Limitations:

Docker is available under two different license models: the Docker Community Edition (CE) is licensed under the Apache License 2.0, while the Docker Enterprise Edition (EE) is licensed under a proprietary license.

The Apache License 2.0 is a permissive open-source license that allows users to use, modify, and distribute Docker CE, both commercially and non-commercially, without any limitations. This license also provides patent protection for users of Docker CE.

However, the proprietary license used by Docker EE may have limitations depending on the terms of the license agreement. Users must review the terms of the license agreement carefully to understand the specific limitations and restrictions.

In general, if you are using Docker CE, you can use it without any license limitations for both commercial and non-commercial purposes. If you are using Docker EE, you should review the license agreement carefully to understand the specific limitations and restrictions that apply to your use case.



###Conclusions:

For a proof of concept (POC), any of the three solutions (Minikube, Kind, or k3d) could work depending on your specific needs and preferences. However, if you are looking for a solution that is easy to set up and use, I would recommend either Minikube or k3d.

Minikube is a popular choice for POCs because it is easy to set up and provides a full Kubernetes environment that you can use to test your application. It also supports multiple hypervisors, so you can choose the one that works best for your environment.

k3d is also a good option for POCs because it is fast and easy to set up. It is designed specifically for local development and testing, so it provides a lightweight Kubernetes distribution that you can use to test your application.

Ultimately, the best solution for your POC will depend on your specific needs and requirements. I would suggest Minikube and deploy it under virtualbox hypervisor. 


### Demo:

1. Create a minikube cluster
   ```
   minikube start --driver=virtualbox
   ```
2. Open the Dashboard (Optional)
   ```
   minikube dashboard
   ```
3. Create a Deployment
   ```
   kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
   ```
4. View the Deployment:
   ```
   kubectl get deployments
   ```
5. Create a Service
   ```
   kubectl expose deployment hello-node --type=LoadBalancer --port=8080
   ```
6. On minikube, the LoadBalancer type makes the Service accessible through the minikube service command.
   ```
   minikube service hello-node
   ```

### Clean UP:
```
kubectl delete service hello-node
kubectl delete deployment hello-node
minikube stop
minikube delete
```