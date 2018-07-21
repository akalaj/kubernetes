# WordPress on Kubernetes

This project was started on July 17th, 2018. In an effort to understand Kubernetes, I decided to create a single-node Kubernetes cluster running MySQL + Wordpress.

The below are the steps needed to create a single-node cluster on Debian Stretch.

## Prepare Debian Stretch Linux Environment

The below steps will walk you through the process of adding <b>[kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)</b> & <b>[minikube](https://kubernetes.io/docs/setup/minikube/)</b> to your Debian stretch environment.

<b>1.) Add the kubernetes.io repository to your apt lists</b>

```bash
#Update your repos to ensure there are no existing problems
sudo apt update
#Add GPG key to apt-key to ensure secure access to kubernetes repo
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
#Create repo file to house the kubernetes.io repo address
sudo touch /etc/apt/sources.list.d/kubernetes.list
#Write the kubernetes.io address to your repo file
echo "deb http://apt.kubernetes.io/ kubernetes-stretch main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
#Pull the latest repo data from the newly added kubernetes.io address
sudo apt update
```

The last command here will ensure that your system has access to pull software from the kubernetes.io repos.

<b>2.) Install kubectl from kubernetes.io repos</b>

Now that you have the kubernetes.io repos available on your Debian stretch system, you can now use apt to install the kubectl software.