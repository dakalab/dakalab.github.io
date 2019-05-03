# Install Kubernetes (k8s) on Ubuntu

### Install Docker

```
apt install docker.io -y
```

### Configure Kubernetes Package Repository

```
apt install apt-transport-https software-properties-common curl -y

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add

apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```

### Disable Swap and Install Kubeadm

```
swapoff -a

apt update && apt install kubeadm -y

kubeadm version
```

### Initialize and Start Kubernetes Cluster

```
kubeadm init --pod-network-cidr=172.168.10.0/24

mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

kubectl get nodes
```

### Deploy Flannel as Pod Network

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

kubectl get nodes

kubectl get pods --all-namespaces
```

### Add Worker Nodes to the Cluster

On the slave machine:

```
kubeadm join <arguments-returned-from-init>
```

If you did not save the token and ca cert hash from the output of `init`, then you can run the following commands to get them:

token:

```
kubeadm token list
```

ca cert hash:

```
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
```

*Below is what the `join` command looks like:*

```
kubeadm join <k8s-master-ip>:6443 --token <k8s-token> \
    --discovery-token-ca-cert-hash sha256:<k8s-hash>
```

## Reference

https://www.linuxtechi.com/install-configure-kubernetes-ubuntu-18-04-ubuntu-18-10/

https://kubernetes.io/docs/reference/setup-tools/kubeadm/
