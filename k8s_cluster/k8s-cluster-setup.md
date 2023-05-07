#### Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

#### Pass-ID: X9448776

#### Author: Atakan Çetinkaya

#### Created: 05.05.2023

#### Description: This .md (k8s-cluster-setup.md) File is explaining how to install the kubeadm "ON" all Nodes

#### File Name: k8s-cluster-setup.md

#### Version: v1.0

---

1.0) These settings are required when setting up a Kubernetes cluster, they allow pods to communicate with each other over the network.

NOTE: Execute command - “ON ALL NODES”

```sh
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```

---

2.0) This command is applying any changes made to the kernel parameters in the configuration files on the system-wide level.

NOTE: Execute command - “ON ALL NODES”

```sh
sudo sysctl --system
```

---

3.0) This command updates the package lists and installs "apt-transport-https" and "curl", which are required for downloading and installing software on Ubuntu and other Debian-based systems.

NOTE: Execute command - “ON ALL NODES”

```sh
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
```

---

4.0) This command downloads the Google Cloud public key for "apt-secure" and adds it to the list of trusted keys on the system, which is
necessary to install software packages from the Google Cloud repositories using.

NOTE: Execute command - “ON ALL NODES”

```sh
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

---

5.0) This command creates a new file named Kubernetes. list in the "/etc/apt/sources.list.d/" directory and adds a new package repository entry for Kubernetes to the file, which is necessary for installing Kubernetes packages using "apt-get".

NOTE: Execute command - “ON ALL NODES”

```sh
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

---

6.0) "sudo apt-get update" is an important step to ensure that your Ubuntu or Debian-based system is up-to-date and has access to the latest
available software packages.

NOTE: Execute command - “ON ALL NODES”

```sh
sudo apt-get update
```

---

7.0) The command "sudo apt-get install -y kubelet kubeadm kubectl" is used to install the Kubernetes components kubelet, kubeadm, and kubectl on a Debian or Ubuntu Linux system.

NOTE: Execute command - “ON ALL NODES” | This command installs the latest Versions of the components

```sh
sudo apt-get install -y kubelet kubeadm kubectl
```

---

8.0) The "sudo apt-mark hold/unhold kubelet kubeadm kubectl" command is used to either "hold" or "unhold" the specified packages in the
Debian/Ubuntu package management system. When a package is "held" it means that the package will not be automatically upgraded to a
newer version when the system is updated using the "apt-get upgrade" command.

NOTE: Execute command - “MASTER NODE”

```sh
sudo apt-mark unhold kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

---

#### Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

#### Pass-ID: X9448776

#### Author: Atakan Çetinkaya

#### Created: 03.05.2023

#### Description: This .md (k8s-cluster-setup.md) File is explaining how to Decide a Node to a "Control Plane" on the cluster

#### File Name: k8s-cluster-setup.md

#### Version: v1.0

---

1.0) The "sudo apt-get install docker.io" command installs the Docker containerization platform on a Debian or Ubuntu Linux system.

NOTE: Execute command - "ON ALL NODES"

```sh
sudo apt-get install docker.io
```

---

2.0) The "sudo kubeadm init --pod-network-cidr=192.168.0.0/16" command initializes a Kubernetes cluster with the specified Pod network
CIDR using kubeadm, which is a tool for bootstrapping Kubernetes clusters.

NOTE: Execute command - "MASTER NODE"

```sh
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

---

3.0) This is a series of commands used to configure the Kubernetes command-line tool kubectl to connect to a Kubernetes cluster that was
initialized using kubeadm.

NOTE: Execute command - "MASTER NODE"

```sh
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

---

4.0) The Tigera Operator is a Kubernetes operator that simplifies the deployment and management of the Calico network security and
connectivity solution in Kubernetes clusters, enabling you to secure and connect your applications with ease.

## NOTE: Execute both command's - "MASTER NODE"

```sh
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/tigera-operator.yaml
```

4.1) The "custom-resources.yaml" file defines the custom resources that are necessary to fully configure and manage the Calico solution in a Kubernetes cluster. When this file is applied using kubectl create -f, it creates these custom resources in the Kubernetes API, enabling you to manage Calico components using Kubernetes-native tools and interfaces.

```sh
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/custom-resources.yaml
```

---

5.0) After doing step "3.0" you should be able to join with the Worker-Nodes into the Cluster through the "Token".

NOTE: Execute command - "WORKER NODES"

```sh
sudo kubeadm join 10.128.0.7:6443 --token m6v2c6.exxrfsgksqcf5tm \ --discovery-token-ca-cert-hash sha256:4890227f4cefd1cffd7dae7430ba1882c106086eaf3ccbd05c665afeb356f
```
