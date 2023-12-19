ifconfig
ifconfig enp0s3
sudo down enp0s3
sudo ifup enp0s3

ping -c 5 google.com  ===> send only 5 count package

wget 
curl




Api Server 
Scheduler: Decide on which node pod run
controller: Managing desired no. of pod is running.

kubelet: manange containers(creation and deletion) created by k8's
KubeProxy: Manage networks of pods created on diff nodes
 
 
Deployment
ReplicaSet/
Maintaining Desired no. of pods running on cluster


Pods

Node
===========================================================
kubectl run fisrtpod --generator=run-pod/v1 --image=coolgourav147/nginx-custom
kubectl run fisrtpod --dry-run --generator=run-pod/v1 --image=coolgourav147/nginx-custom -o yaml >> secondpod.yml
kubectl get pod -o wide

kubectl get pod -o yaml
kubectl get pod -o json

kubectl explain pods|less

kubectl explain pods --recursive|less

kubectl describe pod-name|less
kubectl label pod podname env=testing
kubectl label pod podname env1=dev
kubectl label --overwrite pod podname env=testing
kubectl label pod podname env1-

kubectl label pods -all status=xyz

kubectl get pods --show-labels

kubectl delete pods --all

kubectl describe pod|less


apiVersion: v1
kind: Pod
metadata:
  name: myfirstpod
  labels:
    env: prod
spec:
  containers:
    - name: containername
      image: dignity26/imagename
      env:
        - name: myname
          value: ajit

        - name: age
          value: twentynine



kubectl create -f firstpod.yml
kubectl edit pod firstpod.yml

kubectl create -f firstpod.yml --dry-run

kubectl delete pod firstpod.yml
kubectl delete pod firstpod.yml
kubectl delete -f firstpod.yml
kubectl apply -f firstpod.yml
kubectl apply -f firstpod.yml --server-dry-run
kubectl diff -f firstpod.yml --server-dry-run

to see env variable
docker container exec -it container_id env

kubectl exec -it myfirstpod env
kubectl exec -it myfirstpod -c containername env  (when multiple container inside pod)

kubectl exec myfirstpod -it bash
kubectl exec myfirstpod -c containername -it bash
kubectl exec myfirstpod -c containername -it ls /


init container == It will execute first

ClusterPort: Within Cluster only
kubectl expose pod thirdpod --port=8000 --target-port=80 --name=myfirstservice
port = clusterport
--target-port= Pod port

NodePort: Available from out Side
kubectl expose pod thirdpod --type=Nodeport --port=8000 --target-port=80 --name=myfirstservice


Replication controller====

kubectl create -f replicationcontroller.yml
kubectl delete rc firstreplicationcontroller

kubectl delete rc --cascade=false firstreplicationcontroller (Without deleting Pods)

scaling:
kubectl scale rc --replicas=5 firstreplicationcontroller
kubectl edit rc firstreplicationcontroller
kubectl replace -f replicationcontroller.yml

Replicaset: 
replicaset is Advance (selector is mandatory)

Deployment======
Strategies
1.Recreate 
2.Rolling Update


kubectl rollout status deployment firstdeploy

kubectl rollout 
history  pause restart resume status undo 


kubectl rollout history deployment firstdeploy

kubectl apply -f firstdeployment.yml --record

kubectl rollout undo deployment firstdeploy

kubectl rollout undo --help 


kubectl rollout undo --to-revision=2 deployment firstdeploy

kubectl rollout pause deployment firstdeploy

kubectl rollout resume deployment firstdeploy

docker container stats cont_id.

kubectl api-resources|less

kubectl create ns test

kubectl apply -f pod4.yml --namespace test

kubectl get pods -n test
kubectl get pods --all-namespaces
kubectl get pod -n test

different namespace:
kubectl cluster-info
kube-public = Publically accessible
kube-system = System Resources management
kube-node-lease = nodes

Change default Namespace:
-Kubectl config set-context --current --namespace=test

kubectl exec -n test -it testnswebserver --bash

servicename.namespacesname.svc.cluster.local

kubectl describe ns myns
kubectl 

kubectl apply -f Quota.yml --namespace=myns

limit Range= To set default limits to pods

Config Map:
kubectl create cm cm1 --from-literal=database_ip="192.168.*.*" --from-literal=database_user="root" --from-literal=database_password="mypasswd" 

kubectl create cm cm3 --from-file=application.properties

kubectl create cm cm3 --from-file=properties/

kubectl create cm cm3 --from-env-file=env.sh


Secret:
kubectl create secret --help

kubectl create secret generic firstsecret --from-literal=name=ajit

echo -n "ajit" | base64

kubectl create secret generic filesecret --from-file

kubectl create secret generic fromenvfile --from-file=env.sh

Taint:
kubectl taint node worker01 mysize=large:NoSchedule / PreferNoSchedule /NoExecute
kubectl taint node worker01 mysize-     to remove taint


Volume:
emptyDir: Inside Pod
HostPath: Outside Pod

EKS >> 

eksctl create cluster --name ajit-cluster --node-type t2.small --region ap-south-1 --node-zones ap-south-1a 


Ingress:
Path Based Routing
Host based routing
SSl certificate

Stateful State:
the resources which are allow us to deploy and manage stateful applications
Stateful Application:
The application that requires persistent volume.  Ex. Database
Stateless Ex: Web application.









