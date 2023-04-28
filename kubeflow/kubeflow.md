# Set the Kubeflow version you want to install

export KF_VERSION=1.4.1

# Download and extract the kfctl binary

wget https://github.com/kubeflow/kfctl/releases/download/v${KF_VERSION}/kfctl_v${KF_VERSION}_linux.tar.gz
tar -xvf kfctl_v${KF_VERSION}\_linux.tar.gz
sudo mv kfctl /usr/local/bin/
