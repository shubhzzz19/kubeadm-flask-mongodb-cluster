# Kubernetes Microservice Cluster Flask Application With MongoDB  

This is a microservice application built using Flask and deployed on Kubernetes. It is designed to demonstrate how to build and deploy microservices on a Kubernetes cluster.

![K8s Cluster](https://github.com/shubhzzz19/kubeadm-flask-mongodb-cluster/assets/73218792/880988e7-0fcd-422b-8742-ae725ab54375)

## Requirements

Create two AWS Linux EC2 instances 
1. kub-master (t2.medium)
2. kub-worker (t2.medium)

## Installation And Kubeadm Setup

1. Paste the bellow commands in both (kub-master and kub-worker)
```
sudo su
apt update -y
apt install docker.io -y

systemctl start docker
systemctl enable docker

curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg
echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' > /etc/apt/sources.list.d/kubernetes.list

apt update -y
apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
```

2. Paste the bellow commands in kub-master
```
sudo su
kubeadm init
export KUBECONFIG=/etc/kubernetes/admin.conf
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```

3. Paste the bellow commands in kub-worker
```
sudo su
```
Take the command from kub-master like below and paste it in the kub-worker
```
kubeadm join 172.31.86.8:6443 --token 0zgde9.n73cvv13wptarbin \
    --discovery-token-ca-cert-hash sha256:02110290e76806b616c13d56be0e6d229a53e58521e6c724c53f6213617c15d1 --v=5
```

4. Paste the bellow commands in kub-master
```
kubectl get nodes
git clone https://github.com/shubhzzz19/kubeadm-flask-mongodb-cluster.git
```

5. Move to the k8s directory with command below
```
cd kubeadm-flask-mongodb-cluster/flask-api/k8s
```

6. Deploy the app and its service by the below commands
```
kubectl apply -f taskmaster.yml
kubectl scale --replicas=3 deployment/taskmaster
kubectl get pods
kubectl apply -f taskmaster-svc.yml
kubectl get svc taskmaster-svc
```

7. Create a Persistant volume by the below commands
```
kubectl apply -f mongo-pv.yml
kubectl get pv mongo-pv
kubectl apply -f mongo-pvc.yml
kubectl get pv mongo-pv
```

8. Create the MongoDB pod and its service 
```
kubectl apply -f mongo-pv.yml
kubectl get pv mongo-pv
kubectl apply -f mongo-pvc.yml
kubectl get pv mongo-pv
kubectl apply -f mongo.yml
kubectl get pods
kubectl scale --replicas=2 deployment/<mongo-pod-name>
```

That's it ! Now your application is successfully deployed in the Kubernetes CLuster using kubeadm
