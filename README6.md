docker --version
kubectl version --client
minikube version

choco install kubernetes-cli
choco install minikube
minikube start --driver=docker
kubectl get nodes

mkdir kubernetes-lab
cd kubernetes-lab

Create a file named nginx-pod.yaml.

apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80

Run these commands in CMD:
kubectl apply -f nginx-pod.yaml
kubectl get pods
kubectl describe pod nginx-pod

To open the Nginx page:
kubectl port-forward pod/nginx-pod 8080:80

Open this in your browser: http://localhost:8080

kubectl create deployment my-nginx --image=nginx
kubectl get deployments
kubectl scale deployment my-nginx --replicas=3
kubectl get pods

6. Create a Service
kubectl expose deployment my-nginx --type=NodePort --port=80
kubectl get services
minikube service my-nginx --url

7. Clean up
kubectl delete pod nginx-pod
kubectl delete deployment my-nginx
kubectl delete service my-nginx
minikube stop
