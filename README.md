# study-jenkins-on-k8s
repo for all files that will be need to roll out Jenkins with helm3 on microk8s

- helm repo add jenkinsci https://charts.jenkins.io
- helm repo update
- kubectl apply -f pv.yaml
- kubectl apply -f jenkins-sa.yaml  
- helm install jenkins -n jenkins -f jenkins-values.yaml jenkinsci/jenkins
- kubectl get pods -n jenkins

to get admin pass:
- $ jsonpath="{.data.jenkins-admin-password}" 
- $ secret=$(kubectl get secret -n jenkins jenkins -o jsonpath=$jsonpath)
- $ echo $(echo $secret | base64 --decode)
to get url:
- $ jsonpath="{.spec.ports[0].nodePort}"
- $ NODE_PORT=$(kubectl get -n jenkins -o jsonpath=$jsonpath services jenkins)
- $ jsonpath="{.items[0].status.addresses[0].address}"
- $ NODE_IP=$(kubectl get nodes -n jenkins -o jsonpath=$jsonpath)
- $ echo http://$NODE_IP:$NODE_PORT/login
for port forward:
- $ microk8s kubectl port-forward --address 10.0.2.15 -n jenkins service/jenkins  8080:8080 &