# Kind Kubernetes
kind is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

---

## Environment
- Centos7 running on VirtualBox
- 2 vCPUs
- 3GB of RAM 
- 20GB free space
- Bridged Adapter

#### IP ADDRESS
`192.168.0.20`

---
## Install Docker
```bash
sudo yum install docker -y
sudo systemctl enable docker
sudo systemctl start docker
```
### If Got Permission Denied Issue
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
# and then restart
```
---
## Install Kubectl
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
mkdir -p ~/.local/bin/kubectl
sudo mv ./kubectl /usr/local/bin
```
---
## Install Kind
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin
```
---
## Deploy Kind Cluster
```bash
kind create cluster --name kind-cluster-riset --config=config.yaml
```
you can also change config.yaml as you need, for reference about the kind configuration, click [here](https://kind.sigs.k8s.io/docs/user/configuration/)

## 
![image](https://d33wubrfki0l68.cloudfront.net/e0f6f1da25268d7a0f4ca71368f5b8ab6ae68102/fcc29/images/kind-create-cluster.png)

---
## Check Kubernetes Cluster
```bash
kind get clusters
kind get nodes
kubectl cluster-info
kubectl get node -o wide
```
### To Print Kubeconfig file
```bash 
kind get kubeconfig
```
merge the output with your local ./kube/config file [OPTIONAL]

---
## Create Proxy Tunnel From Windows Host to VM
```bash
ssh -ND 9090 user@192.168.0.20
```
### Access The Proxy
#### Browser
```bash
/mnt/c/Program\ Files/Google/Chrome/Application/chrome.exe --proxy-server="socks5://localhost:9090"
```
#### Terminal 
```bash
export http_proxy=socks5://127.0.0.1:9090
echo $http_proxy
curl 172.18.0.40 #IP that not accessible from HOST
```

>enjoy the cluster!
---
## source
```bash
https://kind.sigs.k8s.io/
https://kind.sigs.k8s.io/docs/user/quick-start/
https://kind.sigs.k8s.io/docs/user/configuration/
```