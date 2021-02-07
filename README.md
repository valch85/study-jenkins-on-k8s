# study-jenkins-on-k8s
repo for all files that will be need to rollout Jenkins by helm3 on microk8s

- helm repo add jenkins https://charts.jenkins.io
- helm repo update
- kubectl apply -f pv.yaml
- helm install [RELEASE_NAME] jenkins/jenkins [flags]