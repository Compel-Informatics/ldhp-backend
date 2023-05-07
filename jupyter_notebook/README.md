# =======================================================================================================================================

# Project: IPA | L-DHP (Lightweight-Data Hub Plattform)

# Pass-ID: X9448776

# Author: Atakan Çetinkaya

# Created: 05.05.2023

# Description: This .md (README.md) File is explaining how to Set-Up the Jupyter-Notebook

# File Name: README.md

# Version: v1.0

## =======================================================================================================================================

1.0) Create or use the Apply command as follows:

## kubectl apply -f jupyter-nginx-dep.yaml

1.1) The command below creates a config in the directory "/home/compel_informatics/snap/jupyter/6/.jupyter/jupyter_notebook_config.py"

## jupyter notebook --generate-config

1.2) After creating the the step above "1.1)", execute the following command:

## jupyter notebook password

1.3) Then you have to type your chosen password, it looks like "Enter password:" and "Verify password:" then you are good to go:
kUFXQXkLWTqPE3W

---

2.0) With the command "jupyter notebook" on the Master-Node, you should be able to start the jupyter notebook:

## jupyter notebook

2.1) As next you get the URL for the jupyer notebook, which you have to copy and paste it into your URL:

## http://localhost:8889/

3.0) As next you have to start the SSH Tunneling from your Client/Laptop on the GCP where your Cluster is Located:

## ssh -L 8889:localhost:8889 34.65.156.101

3.1) This Tunneling command would be an alternativ, if the port 8889, would be already in use:

## ssh -L 8888:localhost:8888 34.65.156.101

4.0) To access the Container in the Pod, execute "kubectl exec -it <pod-name> <-n namespace> -- /bin/bash" as command:

kubectl exec -it jupyter-nginx -n jupyter -- /bin/bash

4.1) To install directly the components/ml-services on the Container:

## kubectl exec jupyter-nginx -n jupyter -- pip install torch torchvision

# ---------------------------------------------------------------------------------------------------------------------------------------
