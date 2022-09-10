# DEPLOY A KUBERNETES CLUSTER USING ANSIBLE

We will take a look at how to deploy a [Kubernetes](https://kubernetes.io/) cluster (version:1.19.2) on **Centos 7** using **Ansible Playbooks**.

We will use Ansible to deploy a small Kubernetes cluster – with one master node, used to manage the cluster, and one worker node, which will be used to run our docker applications. To achieve this, we will use four Ansible playbooks. These will do the following:

- Install Ansible on Centos 7
- Install Kubernetes and docker on each node
- Configure the Master node
- Join the Worker nodes to the new cluster

## Prepare
```
cd /home
mkdir k8s
```
then copy hosts、install-k8s.yml、master.yml、join-workers.yml to /home/k8s .
```
$ ansible -i hosts all -m ping
172.166.30.110 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
172.166.30.111 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    }, 
    "changed": false, 
    "ping": "pong"
}
```
you will see success.

## Install Ansible
```
yum -y update
yum install epel-release
yum -y install ansible
ansible --version
```

## Install Kubernetes and docker on each node
```
ansible-playbook -i hosts install-k8s.yml
```

## Configure the Master node
```
ansible-playbook -i hosts master.yml
```

## Join the Worker nodes to the new cluster
```
ansible-playbook -i hosts join-workers.yml
```

## Check
On each nodes
```
kubectl get nodes
kubectl get pods
```

Reference:  https://buildvirtual.net/deploy-a-kubernetes-cluster-using-ansible/
