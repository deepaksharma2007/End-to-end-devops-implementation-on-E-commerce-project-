# Step-1: Install docker engine on ubuntu 
#### Add Docker's official GPG key:
```bash 
sudo apt-get update 
sudo apt-get install ca-certificates  curl 
sudo install -m 0755 -d /etc/apt/keyrings 
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc 
sudo chmod a+r /etc/apt/keyrings/docker.asc 
```

#### Add the repository to Apt sources:
``` bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

#### Install the Docker packages
``` sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin ```

##### Verify installation 
``` bash
sudo docker run hello-world
docker ps    //failed
sudo docker ps
```


### Note:-  We need to use "sudo" to run Docker commands. To avoid this, we need to add the "ubuntu" user to the "docker" group 
```$ sudo usermod -aG docker ubuntu ```

Now restart the Docker service or re-login to the ubuntu user, and we can run Docker commands without "sudo"

# Step-2: Install Kubectl 
It is used to interact with Kube API server 
``` curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" ```

##### validate the binary
```bash 
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256" 
 echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```
##### Install kubectl 
```sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl ```

###### To verify 
``` bash
kubectl version           //gives both versions :- kubectl(client)  & k8s tool (server)
kubectl version --client
<img width="1186" height="464" alt="image" src="https://github.com/user-attachments/assets/e5b85be7-214e-4a40-a793-ee46a41f7385" />
