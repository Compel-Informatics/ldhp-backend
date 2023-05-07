#=======================================================================================================================================

# Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

# Pass-ID: X9448776

# Author: Atakan Çetinkaya

# Created: 05.05.2023

# Description: This .md (README.md) File is explaining how to install the the ArgoCD-Dashboard on a K8s-Cluster

# File Name: README.md

# Version: v1.0

#=======================================================================================================================================

---

1.0) First of all just create with the "kubectl" comman a namespace so you can deploy all components in the "argocd" namespace:

## kubectl create ns argocd

1.1) The File "install.yaml" has the manifest data to install the ArgoCD, a known Open-Source-Continuous-Delivery-Tool for Kubernetes:

NOTE: Execute command - “MASTER NODE”

## kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

2.0) The "Linuxbrew" is a packet manager for Linux, it gives users the option, to install sourcecodes and to manage them with ease:

NOTE: Execute command - “MASTER NODE”

## sudo apt install linuxbrew-wrapper

3.0) All of the steps above lead to patching the "argocd-server" service, now you have to execute the command down below:

NOTE: Execute command - “MASTER NODE”

## kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

4.0) Now you have to use the "port-forward" to expose that pod so you can access the ArgoCD Dashboard from the localhost:

## kubectl port-forward svc/argocd-server -n argocd 8080:80

4.1) And at the same time you have to do a tunneling from your Client to the GCP - VM to access the localhost on the K8s Cluster:

## ssh -L 8080:localhost:8080 34.65.141.240

5.0) Before deleting the "argocd-initial-admin-secret" in the "ns" argocd you have get the access token with the following command:

## NOTE: Execute command - “MASTER NODE”

5.1) This command is encoding the Secret fully:

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d

Output: PPSE253jZeKXTwG2compel_informatics@master-node-ipa:~$
VALUE1: PPSE253jZeKXTwG2

---

5.2) Now you have to access through the URL "localhost:8080" the Dashboard from ArgoCD itself, insert into the URL the following line:

## localhost:8080

5.3) Now you should see the ArgoCD Dashboard, if that's the case, you have to insert at the two blank boxes the following values:

Username: admin
Password: PPSE253jZeKXTwG2 ------> or the "Token" which you get after step "5.1/VALUE1/" the secret to access the ArgoCD Dashboard

---

6.0) Now you have to delete the created "argocd-initial-admin-secret" secret in the namespace "argocd" with the following command:

NOTE: Execute command - “MASTER NODE”

## kubectl delete secret argocd-initial-admin-secret -n argocd
