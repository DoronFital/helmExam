
# helmExam

Project Details: Home Technical Task

---------------------------

## **Preparation of Linux VM and Commands:**

**java**:

    apt install openjdk-8-jdk
**Jenkins**:

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    
    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    
    /etc/apt/sources.list.d/jenkins.list'
    
    sudo apt-get update
    
    sudo apt-get install jenkins
    
    sudo usermod -a -G docker jenkins

  

**Azure Cli**:

    apt-get update && apt-get install -y libssl-dev libffi-dev python3-dev build-essential
    
    curl -L https://aka.ms/InstallAzureCli | bash

  

**JQ**:

jq (for troubleshooting/making json outputs readable if needed)

    apt-get install jq


**Docker**:

    docker-ce (for az acr login to work properly which is relayed on it)
    
    sudo apt-get install \
    
    apt-transport-https \
    
    ca-certificates \
    
    curl \
    
    gnupg \
    
    lsb-release
    
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    
    echo \
    
    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    apt-get update
    
    apt-get install docker-ce docker-ce-cli containerd.io

**Kubernetes Tools:**

**kubectl**:

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

 
* lib was specified to: /var/lib/azure-cli
* bin was specified to: /usr/bin

**helm (v3)**

    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
    
    chmod 700 get_helm.sh
    
    ./get_helm.sh

**keda**

helm repo add kedacore https://kedacore.github.io/charts

    helm repo update
    
    kubectl create namespace keda
    
    helm install keda kedacore/keda --version 1.4.2 --namespace keda

-------------------------
  
**Restarted Shell:**

    exec -l $SHELL

  
passkey for jenkins for initial login:

    cat /var/lib/jenkins/secrets/initialAdminPassword:
* installed suggested plugins
------------
  
**CLI Logins**

    az login --identity

**AKS Cluster**:

    az aks get-credentials --resource-group devops-interview-rg --name doron-interview-aks --admin

**ACR Login**:

    az acr login --name acrinterview.azurecr.io

  

**creating ingress controller**

used (partially) as reference (https://docs.microsoft.com/en-us/azure/aks/ingress-basic)

	kubectl create namespace ingress-basic 

	helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
	
	helm install nginx-ingress ingress-nginx/ingress-nginx \
	--namespace ingress-basic \
	--set controller.replicaCount=1 \
	--set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
	--set controller.admissionWebhooks.patch.nodeSelector."beta\.kubernetes\.io/os"=linux \
	--set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux


**Helm Chart Creation:**  
  

    helm create simple-web for initial helm package creation

    helm upgrade --install aks-simpleweb --namespace ingress-basic .

* Note: I have set on Chart.yaml "Latest", I would not recommaand doing that on real prod env

  
**Jenkins URL**
	http://52.166.162.90:8080
