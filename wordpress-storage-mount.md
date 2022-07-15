# AZURE Kubernetes Automation

# Fixing storage mount issues

# helm installation

```
wget https://get.helm.sh/helm-v3.6.3-linux-amd64.tar.gz
tar -xvf helm-v3.6.3-linux-amd64.tar.gz
mv linux-amd64/helm /usr/bin/helm
helm version
```

# Starting the WordPress installation

Let's start by installing WordPress. We will demonstrate how it works and then verify that storage is still present after a reboot.


# add the Helm repository for Bitnami:
helm repo add bitnami https://charts.bitnami.com/bitnami

# Begin reinstallation by using the following command:

helm install wp bitnami/wordpress -n k8sdemo

- This will take a couple of minutes to process. You can follow the status of this installation by executing the following command:


watch -n 1 kubectl get all -o wide -n k8sdemo


# login wordpress

- Helm showed you the commands you need to get the admin credentials for our WordPress site. Let's grab those commands and execute them to log on to the site as follows:
```
helm status wp
echo Username: user
kubectl get secret --namespace k8sdemo wp-wordpress -o jsonpath="{.data.wordpress-password}" | base64 -d
```

http://20.121.146.230/admin

username - user
password - JHNzMBMsGr

# Kill the two pods that have the PVC mounted: 

kubectl delete pod --all -n k8sdemo

- As you can see, the two original pods went into a Terminating state. Kubernetes quickly started creating new pods to recover from the pod outage. The pods went through a similar life cycle as the original ones, going from Pending to ContainerCreating to Running.


# after pods recreated go to virtual machine scale sets and stop some of the nodes.

--------------------------------------------------------------------------------------------------------------------
# storage

kubectl create ns twitter

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/3-storage.yml

kubectl apply -f 3-storage.yml

kubectl get pods -n twitter -o wide

kubectl describe pod/database -n twitter


# check the directory has been created to that node

ls -ltrh /var/lib/postgres

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/3-storage.yml

****************************************************************************************************************************************
# multi storage
```
kubectl create ns facebook
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/4-multistorage.yml

kubectl get pods -n facebook -o wide
kubectl get all -n facebook -o wide

kubectl describe pod/db -n facebook

kubectl exec -it pod/db bash -n facebook -c web
kubectl exec -it pod/db bash -n facebook -c db

ls -ltrh /var/www/html/
ls -ltrh /var/lib/postgres

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/4-multistorage.yml
```

***************************************************************************************************************************************
```
kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/5-full.yaml

kubectl get pods -n twitter -o wide
kubectl get all -n twitter -o wide

kubectl describe pod/webserver -n twitter

kubectl exec -it pod/webserver bash -n twitter -c web

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/5-full.yaml
```
***************************************************************************************************************************************
# find out the below yaml file is deployed to which name space

kubectl apply -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/6-example.yml -n cloudnloud

kubectl create ns cloudnloud

kubectl get all -n cloudnloud
kubectl get pod/first-pod -n cloudnloud
kubectl describe pod first-pod -n cloudnloud

kubectl delete -f https://raw.githubusercontent.com/cloudnloud/Kubernetes_Admin_Training/main/class4-namespace-Pod/pod/6-example.yml -n cloudnloud
```
********************************************************************************************
```
kubectl get ns

kubectl delete ns <namespace>
```


