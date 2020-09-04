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

You can optionally install Kubernetes dashboard as follows:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

Kubernetes dashboard can be accessed as follows:
```
kubectl proxy
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```

Create service account as follows:
```
kubectl apply -f service-account.yaml
```

Create cluster role binding as follows:
```
kubectl apply -f cluster-role-binding.yaml
```

To login Kubernetes dashboard, generate bearer token as follows:
```
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```

Copy and paste the token in login screen.

To install ingress controller with Helm:
```
helm install my-release bitnami/nginx-ingress-controller --set hostNetwork=true,service.type=NodePort
```

Sample ingress configuration:
```
apiVersion: extensions/v1beta1
  2   kind: Ingress
  3   metadata:
  4     annotations:
  5       kubernetes.io/ingress.class: nginx
  6     name: example
  7     namespace: default
  8   spec:
  9     rules:
 10       - host: streamer.mngaonkar.com
 11         http:
 12           paths:
 13             - backend:
 14                 serviceName: go-video-streamer-service
 15                 servicePort: 80
 16               path: /
```
