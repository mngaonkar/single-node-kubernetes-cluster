### Create single node Kubernetes cluster

Install kubernetes by running Ansible playbook

```
ansible-playbook playbook.yml
```

Check the cluster state by running kubectl command in virtual machine.
```
kubectl get nodes
```

Copy kubernetes config (~/.kube/config) from virtual machine to local machine. Set environment variable KUBECONFIG to point to config file. Now you can run kubectl command from local machine to manage kubernetes cluster.
