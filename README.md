
# KUBEADM-TO-CREATE-CLUSTER

### => Ports that need to enable on both Master and Worker nodes:

| Protocal | Direction | Port-Range  | Purpose                 | Used By               |
|----------|-----------|-------------|-------------------------|-----------------------|
| TCP      | Inbound   | 6443*       | Kubernetes API server   | All                   |
| TCP      | Inbound   | 2379- 2380  | etcd server client api  | kube-apiserver , etcd |
| TCP      | Inbound   | 10250       | Kubelet API             | Self control,plane    |
| TCP      | Inbound   | 10251       | Kube-Schedular          | Self                  |
| TCP      | Inbound   | 30000-32767 | Nodeport-services+      | All                   |
| TCP      | Inbound   | 10252       | Kube-controller manager | Self                  |
| TCP      | Ibound    | 22          | SSH                     | Self                  |
| TCP      | Ibnound   | 80          | HTTP                    | Self                  |
| TCP      | Inbound   | 443         | HTTPS                   | Self                  |
| TCP      | Inbound   | 5432        | Postgres                | postgres              |

#### => Otherwise you can also allow the all tcp.

### Step 1: Enter this command on both Master and Worker nodes:
```bash
 
sudo su  // Take the super user access 

setenforce 0

To disable SELinux temporarily (disable the security of Linux)

```
### Step 2: Enter this command on both Master and Worker nodes:
```bash
 free -h 

The free command gives information about used and unused memory usage and swap memory of a system.

```
### Step 3: Enter this command on both Master and Worker nodes:
```bash
  
swapoff -a

To deactivate a swap space, use the command swapoff

```
### Step 4: Enter this command on both Master and Worker nodes:
```bash
cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```
#### Step 5: Enter this command on both Master and Worker nodes:
```bash
yum install docker 

systemctl enable docker 

systemctl start docker 
```
### Step 6: Enter this command on both Master and Worker nodes:
```bash
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
       https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```
### Step 7: Enter this command on both Master and Worker nodes:
```bash
 yum install kubeadm kubectl kubelet
```
### Step 8: Enter this command only on Master Node:
```bash
 kubeadm init
```
### Step 9: When you execute kubeadm init command then it gives a token copy that and enter below commands on master :
```bash
 
mkdir -p $HOME/.kube
 
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
### Step 10: Now paste the token on Worker Nodes to connect with Master Node.

### Then Worker node connecting successfully now use the kubectl command!!!!!
