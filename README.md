This project demonstrates how to deploy Jenkins on a Kubernetes cluster using Minikube and Kubernetes manifest files. The deployment includes a Jenkins Deployment, Service, and PersistentVolumeClaim for data persistence
Prerequisites
Before proceeding, ensure the following tools are installed:

Minikube: A local Kubernetes cluster.
kubectl: Kubernetes command-line tool.
Docker: Required for Minikube to run containers.

Steps to Deploy Jenkins
1. Start Minikube
Start a Minikube cluster. Use the following command to start the minikube cluster:
minikube start
Verify the cluster is running by using the following code:
minikube status
2. Create a dedicated namespace for Jenkins. This is to help you organize your deployments:
   kubectl create namespace jenkins
   
3. Deploy Jenkins Using Kubernetes Manifests
a. PersistentVolumeClaim (PVC)
Create and apply jenkins-pvc.yaml file to persist Jenkins data:
b. create and apply jenkins deployment file
c. Create and apply jenkins service file
4.  Access Jenkins
   a. Get the Minikube IP: minkube ip
   b. Access the deployment on browser: http://<minikube-ip>:<service Nodeport>
   c. Retrieve the jenkins admin password: kubectl exec -n jenkins <jenkins-pod-name> -- cat /var/jenkins_home/secrets/initialAdminPassword
   d. To get the pod name: use kubectl get pods -n jenkins to find it
   e. Paste the password into the Jenkins setup wizard and complete the installation.
5. Clean up:
kubectl delete -f jenkins-deployment.yaml
kubectl delete -f jenkins-service.yaml
kubectl delete -f jenkins-pvc.yaml
kubectl delete namespace jenkins

   Notes:
   This setup is intended for local development and testing using Minikube.
For production environments, consider using a cloud provider, enabling TLS, and configuring backups.
PersistentVolumeClaim ensures Jenkins data is retained even if the pod is restarted.

