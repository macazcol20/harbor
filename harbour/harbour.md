```sh
kubectl create namespace harbor

helm repo add harbor https://helm.goharbor.io
helm repo update
helm search repo harbor
helm pull  harbor/harbor --untar=true
helm install harbor ./harbor -n harbor -f harbor-values.yaml

# helm install harbor ./harbor -n harbor -f harbor-values.yaml --set nginx.replicas=0
helm upgrade --install harbor harbor/harbor --namespace harbor
helm uninstall harbor --namespace harbor
k -n harbor delete pvc --all
```

```sh
sudo sh docker.sh
sudo usermod -aG docker cafanwii
newgrp docker
docker version
docker run hello-world
```

```sh
sudo docker login https://harbor.pixiescloud.com
docker pull nginx:alpine
docker tag nginx:alpine harbor.pixiescloud.com/library/nginx:alpine
docker push harbor.pixiescloud.com/library/nginx:alpine
## OR CREATE PACKAGE CALLED pixieharbor
sudo docker login https://harbor.pixiescloud.com
docker pull nginx:alpine
docker tag nginx:alpine harbor.pixiescloud.com/pixieharbor/nginx:alpine
docker push harbor.pixiescloud.com/pixieharbor/nginx:alpine
```


## private harbor project:
```sh
- Go to your project → Robot Accounts tab.
- Click "New Robot Account"
- Assign it permissions (e.g., push/pull).
- Save the username and token (robot$<name>, and its token).

## login
docker login harbor.pixiescloud.com -u robot$myrobot -p xxxx
docker tag nginx:alpine harbor.pixiescloud.com/privateproject/nginx:alpine
docker push harbor.pixiescloud.com/privateproject/nginx:alpine

## If pulling in Kubernetes, you'll need to create a Secret:
kubectl create secret docker-registry harbor-secret \
  --docker-server=harbor.pixiescloud.com \
  --docker-username=robot$myrobot \
  --docker-password=xxx \
  --namespace=my-namespace
```



Username: admin 
Password: Harbor12345 


kubectl -n harbor get svc