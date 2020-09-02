Build the container:
```
git clone --recurse-submodules https://github.com/mathieu-benoit/myblog
docker build -t blog .
```

Run locally:
```
docker run -d -p 8080:8080 blog
```

Deploy on Kubernetes:
```
kubectl create ns myblog
kubectl config set-context --current --namespace myblog

# Simple way with just a deployment and service:
kubectl apply -f k8s/deployment.yaml # you need to change the container image reference accordingly.
kubectl apply -f k8s/service.yaml # you need to change the type of the service accordingly.

# Complete way:
kubectl apply -f k8s/
```

Define the Cloud Build trigger:
```
gcloud beta builds triggers create github \
    --repo-name=myblog \
    --repo-owner=mathieu-benoit \
    --branch-pattern="master" \
    --build-config=cloudbuild-ci.yaml
```
