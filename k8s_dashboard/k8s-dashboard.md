#### Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

#### Pass-ID: X9448776

#### Author: Atakan Çetinkaya

#### Created: 03.05.2023 |

#### Description: This .md (k8s-dashboard.md) File is explaining how to setup the K8s-Dashboard on the K8s-Cluster

#### File Name: k8s-dashboard.md

#### Version: v1.0

---

1.0) This URL give's you the latest K8s-Dashboard config, execute the following command like that:

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
```

---

2.0) The Yaml "k8s_access_token.yaml" is also created by "Me", but through various tests I came to the conclusion, it work perfectly:

```sh
kubectl apply -f k8s_access_token.yaml
```

---

3.0) Execute this Command after the Deployment and Secret is created. It reveals the "Secret-Token" to access the K8s-Dashboard:

```sh
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep dashboard-token | awk '{print $1}')
```

3.1) After excuting the command at "3.0" you will get the Token revealed from the Secret at step "2.0":

```sh
eyJhbGciOiJSUzI1NiIsImtpZCI6IjN1Nko4MERBLVRhX0NBbmdTeTZIaWdXTWxuZzlBZndUNFNxcUhDdWhZcjgifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJkYXNoYm9hcmQtdG9rZW4iLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGFzaGJvYXJkLWFkbWluIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiM2JlNWQ3MWEtMGU3Ni00NDcxLWE0OGEtMmVjMmJlYzMwOGRlIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmVybmV0ZXMtZGFzaGJvYXJkOmRhc2hib2FyZC1hZG1pbiJ9.vbGal0CxFnFdtHXYJH21BxQ50XpdJwIQcZnNFapzh3CnKYRiD0IrXy1s8jwOapY61hutWe4LlCAXS3MAys6GLcYZH2XsfMP-UEVd8ccvfhLLK23ZQDwIUj5pe1S7rCYIjRmKJN0EZ2vkJN8KRUqNBxGj6CgwuwNUyy74dERAFeDDIrwHLCA0BQJawkE1MQGqAwom7ICvogtvhg4ihWhmqAfuDnxnSML2wAnGGFHKFRcLPd4Vc-EObwfH0rdaBk3495zPV7xs07I0ntnGCRQqw-7UhkjAtbhbwBmF1BtJY4dlNG6vUp9m5AwjHr9GfNsp2NCOKvN5sNk9ILvEV2VqVg
```

---

4.0) Now start the port-forwarding with the "kubectl" command, the way, that the Role can forward the connection:

```sh
kubectl proxy
```

---

5.0) As next you have to start the SSH Tunneling from your Client/Laptop on the GCP where your Cluster is Located:

```sh
ssh -L 8001:localhost:8001 34.65.141.240
```

---

6.0) Now you can access the Dashboard, with the "Token" from the step Number "3.1", Paste the following Link into the URL:

```sh
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```
