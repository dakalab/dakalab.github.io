# 在 Ubuntu 安装 Kubernetes (k8s)

### 安装 Docker

```
apt install docker.io -y
```

### 设置 Kubernetes 软件包仓库

```
apt install apt-transport-https software-properties-common curl -y

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add

apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```

### 禁用 Swap 并安装 Kubeadm

```
swapoff -a

apt update && apt install kubeadm -y

kubeadm version
```

### 初始化并启动 Kubernetes 集群

```
kubeadm init --pod-network-cidr=172.168.10.0/24

mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

kubectl get nodes
```

### 部署 Flannel 作为 Pod Network

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

kubectl get nodes

kubectl get pods --all-namespaces
```

### 添加工人节点到集群

在工人机器上:

```
kubeadm join <arguments-returned-from-init>
```

如果你没有保存初始化时候输出的token和秘钥，那么你还能通过下面的命令获取他们：

token:

```
kubeadm token list
```

秘钥:

```
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
```

*下面是 `join` 命令的样子：*

```
kubeadm join <k8s-master-ip>:6443 --token <k8s-token> \
    --discovery-token-ca-cert-hash sha256:<k8s-hash>
```

## 参考资料

https://www.linuxtechi.com/install-configure-kubernetes-ubuntu-18-04-ubuntu-18-10/

https://kubernetes.io/docs/reference/setup-tools/kubeadm/
