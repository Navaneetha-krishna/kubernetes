# kubernetes
Run the below commands in all three nodes:
------------------------------------------
- Switch to root user
- sudo su -
- Update the System
- apt-get update
- Install http package
- apt-get install apt-transport-https

Docker Installation
-------------------
- apt install docker.io -y
- docker --version
- systemctl start docker
- systemctl enable docker

Setup open GPG Key
------------------
sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add 

Edit source list file 
---------------------
nano /etc/apt/sources.list.d/kubernetes.list

Add below line in the above file
--------------------------------
deb http://apt.kubernetes.io/ kubernetes-xenial main

Ctrl X
Y
Enter

Install the Kubernetes packages
-------------------------------
- apt-get update
- apt-get install -y kubelet kubeadm kubectl kubernetes-cni


BOOTSTRAPPING THE MASTER NODE (Only in MASTER Node)
---------------------------------------------------
kubeadm init
 
Copy the command to run in Nodes & Save it in a Notepad.
--------------------------------------------------------
Create both .kube and its parent directory (-p)
mkdir -p $HOME/.kube
Copy configuration to kube directory (in config file)
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
Provide user permissions to config file
chown $(id -u):$(id -g) $HOME/.kube/config

Deploy flanner node network for its repository path. Fannel is going to place a binary in each node
-----------------------------------------------------------------------------------------------------
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

Configure Worker Nodes
----------------------
COPY LONG CODE PROVIDED MY MASTER IN NODE NOW LIKE CODE GIVEN BELOW
kubeadm join 172.31.14.32:6443 --token mcvd2n.aqvyp59vq3inhtks --discovery-token-ca-cert-hash sha256:5ab6e6d695d31c05a4e4cde8f6e7b14ff0d0b450383e9b255270be90904de128

GO TO MASTER AND RUN THIS COMMAND
---------------------------------
kubectl get nodes
