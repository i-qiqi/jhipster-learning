# Running Kubernetes locally via Minikube
## Tools
- `kubectl`
- `minikube`

##  Installation
In the process of installing `minikube` , I encountered many weird bug here , too many to enumerate them completely. I think other guys also are plagued by them. many issues can be seen @ <https://github.com/kubernetes/minikube/issues/2818>

- I take a alternative version of minikube and kubernetes.　To my surprise , this case succeeded.  And thinks to [Minikube - Kubernetes本地实验环境](https://yq.aliyun.com/articles/221687?p=2)

  ```bash
  # install minikube
  curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v0.25.2/minikube-linux-      amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
  --kubernetes-version v1.9.4```

## Create a Minikube cluster
- In the previous attempts of `minikube start`, `kubelet` and `kubeadm`  were so slow to download. Also I tried the configure the global proxy with `shadowsocks-qt5`, but it didn't work.
  - [Ubuntu使用Shadowsocks-qt5科学上网](https://my.oschina.net/airship/blog/1812419)
  - [Linux中使用ShadowSocks+Privoxy代理](https://docs.lvrui.io/2016/12/12/Linux%E4%B8%AD%E4%BD%BF%E7%94%A8ShadowSocks-Privoxy%E4%BB%A3%E7%90%86/)
  - [Ubuntu18.04中安装shadowsocks和privoxy全局代理](https://ywnz.com/linuxjc/2687.html)

  ```bash
# minikube
minikube start --registry-mirror=https://registry.docker-cn.com
# set the Minikube context with kubectl
kubectl config use-context minikube
# Verify that kubectl is configured to commucated with the cluster
kubectl cluster-info
```

## Create a Docker container image.
### Reusing the Docker daemon

-  When using a single VM of kuberbetes, it's really handy to reuse the minikube's built-in Docker daemon. As this means you don't have to build a docker registry on your host machine and push the image into it-you can just build inside the same docker daemon as minikube which speeds up local experiments. If you build the image on your mac/linux , with pull image policy of `Always` correspondingly, which may eventually result in `ErrImagePull` as you may not have any versions of your Docker image out there in the default registry(usually Docker Hub) yet.
- To be enable to work with the docker daemon on your mac/linux host use the `docker-env` command in your shell.
```bash
# make sure that point docket client to the the minkube VM's docker daemon .
eval $(minikube docker-env)
# you should now be ablde to use docker on the command line on your host mac/linux machine talking to the docker daemon inside the minkube VM.
# Build your Docker image, using the Minikube Docker daemon(mind the trailing dot)
docker build -t hello-node:v1 .
docker ps
# Note : Later , when you no longer wish to use the Minikube VM host , you can undo the change by running :
eval $(minikube docker-env -u)
```
- References List :
  - [Minikube体验](https://www.cnblogs.com/cocowool/p/minikube_setup_and_first_sample.html)
  - [minikube 安装和使用](http://www.cnblogs.com/yuanchao120/p/9816838.html)

### Create a Deployment
- A Kubernetes *`Pod`* is a group of one or more Containers, tied together for the purpose of administration and networking.
- A kubernetes *`Deployment`*  checks on the health of your Pod and restart the Pod's Container if it terminates. Deployments are the recommanded way to manage the creation and scaling of Pods.
```bash
# create a Deployment and manages a Pod
kubectl run hello-node --image=hello-node:v1 --port=8080
 --image-pull-policy=Never
 # View thw Deployment
 kubectl get deployments
#  View the Pod:
 kubectl get pods
 # View cluster events:
 kubectl cluster events
 # View the kubectk configuration
 kubectl config view
```
### Create a Service
By default, the Pod is only accessible by its  internal IP address within the Kubernetes cluster. To make the Pod accessible from outside the kubernetes virtual network, you have to expose Pod as a `Kubernetes Service`
```bash
# Expose the Pod to the public internet
kubectl expose deployment hello-node --type=LoadBalancer
# View the Service you just created
kubectl get services
# Automatically open up a browser window to using a local IP address that serves your app and shows the result.
minikube service hello-node
```
### Update your app
```bash
docker build -t hello-node:v2
kubectl set image deployment/hello-node hello-node=hello-node:v2
minikube service hello-node
```
### Enable  addons
```bash
minikube addons list
# output
storage-provisioner: enabled
kube-dns: enabled
registry: disabled
registry-creds: disabled
addon-manager: enabled
dashboard: disabled
 default-storageclass: enabled
coredns: disabled
heapster: disabled
efk: disabled
ingress: disabled
# Minikube must be running for these commands to take effect. To enable `heapster` addon
minikube addons enable heapster
# View the Pod and Service you just created
kubectl get po,svc -n kube-system
```
### Clean up
```bash
# delete service
kubectl delete service hello-node
# delete deployment
kubectl delete deployment hello-node
# Optionally, force removal of the Docker images created
docker rmi hello-node:v1 hello-node:v2 -f
# Optionally, stop the Minikube VM
minikube stop
eval $(minikube docker-env -u)
# Optionally, delete the Minikube VM
minikube delete
```
