minikube start --driver=docker
kubectl get nodes

Pull the Python Docker image
Run:
docker pull thetechdarts/sampleflaskapp
mkdir python-kubernetes
cd python-kubernetes

python-deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: python-web-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: python-web
  template:
    metadata:
      labels:
        app: python-web
    spec:
      containers:
      - name: python-web
        image: thetechdarts/sampleflaskapp:latest
        ports:
        - containerPort: 5000


kubectl apply -f python-deployment.yaml
kubectl get deployments
kubectl get pods
kubectl describe deployment python-web-deployment

python-service.yaml

apiVersion: v1
kind: Service
metadata:
  name: python-web-service
spec:
  type: NodePort
  selector:
    app: python-web
  ports:
  - protocol: TCP
    port: 5000
    targetPort: 5000


kubectl apply -f python-service.yaml
kubectl get svc

minikube service python-web-service --url

Cleanup
kubectl delete deployment python-web-deployment
kubectl delete service python-web-service
minikube stop
minikube delete
