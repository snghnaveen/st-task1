### Cluster stepup k8s


```shell
sudo kubeadm init --apiserver-advertise-address=192.168.3.120 --pod-network-cidr=192.168.0.0/16
```

![img.png](img.png)


```shell
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

```shell
sudo kubeadm join 192.168.3.120:6443 --token 03x2vj.rsh80ak7d2owfgv2 \
    --discovery-token-ca-cert-hash sha256:fde92e6f8a15f46d615271936fd9e991ad245ab9aeacd9a002d65b68149252ac  
```

![img_1.png](img_1.png)

```shell
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

![img_2.png](img_2.png)


```shell
kubectl create deployment -f  nginx-pod.yaml
```
![img_3.png](img_3.png)


```shell
kubectl get po
```
![img_4.png](img_4.png)

```shell
kubectl get po -o wide
```
![img_5.png](img_5.png)

```shell
sudo docker ps
```
![img_6.png](img_6.png)


```shell
kubectl create service nodeport nginx --tcp=80:8
```

![img_7.png](img_7.png)

```shell
kubectl get svc
```

![img_8.png](img_8.png)


![img_9.png](img_9.png)


### dashboard ui setup 

```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

```shell
kubectl proxy
```

```shell
kubectl create serviceaccount dashboard -n default
```

```shell
kubectl create clusterrolebinding dashboard-admin -n default  --clusterrole=cluster-admin  --serviceaccount=default:dashboard
```

```shell
kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
```

![img_10.png](img_10.png)


![img_11.png](img_11.png)