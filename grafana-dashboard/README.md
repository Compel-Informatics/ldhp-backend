# =======================================================================================================================================

# Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

# Pass-ID: X9448776

# Author: Atakan Çetinkaya

# Created: 04.05.2023 | 11:35:10

# Description: This .md (README.md) File is explaining how to install Grafana and get access to the Grafana-Dashboard

# File Name: README.md

# Version: v1.0

# =======================================================================================================================================

---

1.0) First step is to get all the Kubernetes manifests (YAML Files) from the URL down below:

## git clone https://github.com/bibinwilson/kubernetes-grafana.git

2.0) As next you create a new Yaml File which is called "grafana_configmap.yaml" it includes an configmap for Grafana:

## vim grafana_configmap.yaml

2.1) After creating the Yaml "grafana_configmap.yaml" you are good to go to "apply -f" it with the kubectl command:

## kubectl apply -f grafana_configmap.yaml

3.0) As next you create a new Yaml File which is called "grafana_deployment.yaml" it includes the Deployment/Pod for Grafana:

## vim grafana_deployment.yaml

3.1) After creating the Yaml "grafana_deployment.yaml" you are good to go to "apply -f" it with the kubectl command:

## kubectl apply -f grafana_deployment.yaml

4.0) As next you create a new Yaml File which is called "grafana_service.yaml" it includes the service to port-forward for Grafana:

## vim grafana_service.yaml

4.1) After creating the Yaml "grafana_service.yaml" you are good to go to "apply -f" it with the kubectl command:

## kubectl apply -f grafana_service.yaml

6.0) This is now the last step to access the Grafana-Dashboard, paste the localhost-URL into the URL bar on your Browser:

## http://34.32.170.249:32005

6.1) Now you should see the Grafana Dashboard, if that's the case, you have insert at the two blank boxes the following values:

Username: admin
Password: wnKZ5z4LV37vR7E

---

## 7.0) You don't have to do any port-forward, if you work with the external IP of the GCP - VM with the Port "32005":

7.1) These steps are not necessary if you access the Grafana-Dashboard over the external IP Address from the Virtual Machine:

ssh -L 3000:localhost:3000 34.65.156.101

kubectl port-forward -n monitoring <grafana-pod-name> 3000:3000

## kubectl port-forward -n monitoring <grafana-pod-name> 3000 &
