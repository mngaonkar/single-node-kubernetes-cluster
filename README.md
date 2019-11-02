### Create single node Kubernetes cluster on Ubuntu 18.04 (1 CPU, 2GB RAM)

Make sure Python 2.7 is installed on Ubuntu 
```
apt-get install python
```

Install Ansible on Ubuntu
```
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

Install kubernetes by running Ansible playbook

```
sudo ansible-playbook playbook.yml
```

Check the cluster state by running kubectl command in virtual machine.
```
kubectl get nodes
```

Copy kubernetes config (~/.kube/config) from virtual machine to local machine. Set environment variable KUBECONFIG to point to config file. Now you can run kubectl command from local machine to manage kubernetes cluster.
