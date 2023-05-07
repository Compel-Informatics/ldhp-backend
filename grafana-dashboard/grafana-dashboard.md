#### Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

#### Pass-ID: X9448776

#### Author: Atakan Çetinkaya

#### Created: 05.05.2023

#### Description: This .md (grafana-dashboard.md) File is explaining how to install the the Grafana-Dashboard on a K8s-Cluster

#### File Name: grafana-dashboard.md

#### Version: v1.0

---

1.0) First step is to get all the Kubernetes manifests (YAML Files) from the URL down below:

```sh
git clone https://github.com/bibinwilson/kubernetes-grafana.git
```

---

2.0) As next you create a new Yaml File which is called "grafana_configmap.yaml" it includes an configmap for Grafana:

```sh
vim grafana_configmap.yaml
```

2.1) After creating the Yaml "grafana_configmap.yaml" you are good to go to "apply -f" it with the kubectl command:

```sh
kubectl apply -f grafana_configmap.yaml
```

---

3.0) As next you create a new Yaml File which is called "grafana_deployment.yaml" it includes the Deployment/Pod for Grafana:

```sh
vim grafana_deployment.yaml
```

3.1) After creating the Yaml "grafana_deployment.yaml" you are good to go to "apply -f" it with the kubectl command:

```sh
kubectl apply -f grafana_deployment.yaml
```

---

4.0) As next you create a new Yaml File which is called "grafana_service.yaml" it includes the service to port-forward for Grafana:

```sh
vim grafana_service.yaml
```

4.1) After creating the Yaml "grafana_service.yaml" you are good to go to "apply -f" it with the kubectl command:

```sh
kubectl apply -f grafana_service.yaml
```

---

5.0) This is now the last step to access the Grafana-Dashboard, paste the localhost-URL into the URL bar on your Browser:

```sh
http://34.32.170.249:32005
```

5.1) Now you should see the Grafana Dashboard, if that's the case, you have insert at the two blank boxes the following values:

```sh
Username: admin
Password: wnKZ5z4LV37vR7E
```

---

6.0) You don't have to do any port-forward, if you work with the external IP of the GCP - VM with the Port "32005":

```sh
kubectl port-forward -n <namespace> <grafana-pod-name> 3000:3000
kubectl port-forward -n <namespace> <grafana-pod-name> 3000 &
```

6.1) These steps are not necessary if you access the Grafana-Dashboard over the external IP Address from the Virtual Machine:

```sh
ssh -L 3000:localhost:3000 34.65.156.101
```
