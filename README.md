# ansible_local
Uses an ansible-playbook to deploy a K8s cluster to minikube on OSX

## Pre-requistes

* minikube
* Ansible
* cloudflared

Use homebrew to install these.

```
brew install minikube
brew install ansible
brew install cloudflare/cloudflare/cloudflared
```

Affiliate `cloudflared` with your Cloudflare account by running the following

```
cloudflared tunnel login
```

You can verify these tools are installed correctly by running the following

```
cloudflared --version
ansible --version
minikube status
```

## Usage
1. Set a DOMAIN variable for the endpoint. I have my tunnel tied to chrisdlg.com so my workflow looks like this

```
❯ export DOMAIN="local.chrisdlg"
❯ env | grep -i domain
DOMAIN=local.chrisdlg
```

2. Clone this repository.

_Example using SSH to clone repo_

```
git clone git@github.com:tenaciousdlg/ansible_local.git
```

3. Run ansible-playbook

_Note that this is ran from the same directory (folder) that `main.yaml` is located_

```
❯ ansible-playbook  -i hosts main.yaml

PLAY [minikube cloudflared local k8s] *****************************************************************************************************************************************************

```

4. When you're done remove the cluster via minikube

```
❯ minikube delete
🔥  Deleting "minikube" in docker ...
🔥  Deleting container "minikube" ...
🔥  Removing /Users/dlg/.minikube/machines/minikube ...
💀  Removed all traces of the "minikube" cluster.
```