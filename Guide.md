# Pre-requisites 
We need to either install UTM or VMWare Fusion Player
- [VMWare Fusion Player](https://www.vmware.com/sg/products/fusion/fusion-evaluation.html) 
- [UTM](https://mac.getutm.app/)

# Downloading ISO
We will be downloading the Jammy JellyFish version of Ubutunu
- [jammy-desktop-arm64.iso](https://cdimage.ubuntu.com/jammy/daily-live/pending/)

# Running it on VM
*(Note) We will be doing it on VMWare Fusion*
Steps
1. Open VMware Fusion Player and click the plus button and press New ![](https://i.imgur.com/U5xwCm4.png)
2. Afterwards click the install from disc or image![](https://i.imgur.com/37zD4Vv.png)
3. Drag your iso file you downloaded and click continue until you are finished
4. You will be brought to this screen now, press enter to install ![](https://i.imgur.com/OgPMq23.png)
5. Double click the **Install Ubuntu** desktop icon or find the icon at the left bar 
   ![](https://i.imgur.com/IsvzOe0.png) 
7. Leave everything with the default settings and keep pressing continue 
8. When you reach the credentials page you can use these credentials in the guide *(Optionally set Login automatically)* ![](https://i.imgur.com/3yREalB.png)
9. After you have restarted your Ubuntu VM, press enter to boot.
10. Now enter your credentials from Step 8 and you will be inside your fully functional Ubuntu VM

# Install Docker
Taken from this guide
- [How to Install Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)
	- Following **Install using the `apt` directory**

Follow in order
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Execute Docker without Sudo
Follow in order
```bash
sudo usermod -aG docker ${USER}

su - ${USER}
```

## Checking if Docker works
```bash
docker run hello-world #checks if docker is working
```

# Install Kubernetes
Taken from this guide 
- [Install Kubernetes Documentaiton](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

kubectl version --client

kubectl version --client --output=yaml
```

## What is a Control Plane
In order to run `kubectl` commands to create pods and many others. We need a control plane which helps manage clusters and resources
- We will be installing **MiniKube** as our control plane
![](https://i.imgur.com/pybn22F.png)

## Install Minikube 
Taken from this guide
- [Install Minikube Documentation](https://minikube.sigs.k8s.io/docs/start/)

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-arm64

sudo install minikube-linux-arm64 /usr/local/bin/minikube && rm minikube-linux-arm64

minikube start
```

## Checking if everything works
This should output the same as the step where we used the `Docker` command to run the container
```bash
kubectl run hello --restart=Never --image=hello-world -it
```
