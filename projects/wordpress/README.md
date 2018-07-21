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

```bash
#Install kubectl
sudo apt install kubectl
```

You can confirm that the installation is working by requesting kubectl to print the version

```java
akalaj@node1:~$ kubectl version
Client Version: version.Info{Major:"1", Minor:"6", GitVersion:"v1.6.0", GitCommit:"fff5156092b56e6bd60fff75aad4dc9de6b6ef37", GitTreeState:"clean", BuildDate:"2017-03-28T16:36:33Z", GoVersion:"go1.7.5", Compiler:"gc", Platform:"linux/amd64"}
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```

<b>3.) Install minikube from kubernetes.io using curl</b>

<b>Minikube</b> is a binary that we need to have present on our machine. We will pull the amd64 version of the binary directly from the googleapis repo using curl. Once it's in usr/local, we'll have the ability to call it from anywhere.

```bash
#Download and place minikube binary in /usr/local/bin
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.28.1/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
To verify that minikube is working, try and extract the version.

```java
akalaj@worknode:~/personal/kubernetes$ minikube version
minikube version: v0.28.1
```

## Setting The Stage For Wordpress on Kubernetes (file configuration)

Test, test, test