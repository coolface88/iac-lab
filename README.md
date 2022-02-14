# Infrastructure as Code


### Tech stack

<table>
  <tr>
    <th>Logo</th>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><img width="32" src="https://simpleicons.org/icons/ansible.svg"></td>
    <td><a href="https://www.ansible.com">Ansible</a></td>
    <td>Automate bare metal provisioning and configuration</td>
  </tr>
  <tr>
    <td><img width="32" src="https://cncf-branding.netlify.app/img/projects/argo/icon/color/argo-icon-color.svg"></td>
    <td><a href="https://argoproj.github.io/cd">ArgoCD</a></td>
    <td>GitOps tool built to deploy applications to Kubernetes</td>
  </tr>
  <tr>
    <td><img width="32" src="https://www.docker.com/sites/default/files/d8/2019-07/Moby-logo.png"></td>
    <td><a href="https://www.docker.com">Docker</a></td>
    <td>Ephermeral PXE server and convenient tools container</td>
  </tr>
  <tr>
    <td><img width="32" src="https://upload.wikimedia.org/wikipedia/commons/b/bb/Gitea_Logo.svg"></td>
    <td><a href="https://gitea.com">Gitea</a></td>
    <td>Self-hosted Git service</td>
  </tr>
  <tr>
    <td><img width="32" src="https://grafana.com/static/img/menu/grafana2.svg"></td>
    <td><a href="https://grafana.com">Grafana</a></td>
    <td>Operational dashboards</td>
  </tr>
  <tr>
    <td><img width="32" src="https://cncf-branding.netlify.app/img/projects/helm/icon/color/helm-icon-color.svg"></td>
    <td><a href="https://helm.sh">Helm</a></td>
    <td>The package manager for Kubernetes</td>
  </tr>
  <tr>
    <td><img width="32" src="https://cncf-branding.netlify.app/img/projects/k3s/icon/color/k3s-icon-color.svg"></td>
    <td><a href="https://k3s.io">K3s</a></td>
    <td>Lightweight distribution of Kubernetes</td>
  </tr>
  <tr>
    <td><img width="32" src="https://cncf-branding.netlify.app/img/projects/kubernetes/icon/color/kubernetes-icon-color.svg"></td>
    <td><a href="https://kubernetes.io">Kubernetes</a></td>
    <td>Container-orchestration system, the backbone of this project</td>
  </tr>
  <tr>
    <td><img width="32" src="https://github.com/grafana/loki/blob/main/docs/sources/logo.png?raw=true"></td>
    <td><a href="https://grafana.com/oss/loki">Loki</a></td>
    <td>Log aggregation system</td>
  </tr>
  <tr>
    <td><img width="32" src="https://avatars.githubusercontent.com/u/60239468?s=200&v=4"></td>
    <td><a href="https://metallb.org">MetalLB</a></td>
    <td>Bare metal load-balancer for Kubernetes</td>
  </tr>
  <tr>
    <td><img width="32" src="https://avatars.githubusercontent.com/u/1412239?s=200&v=4"></td>
    <td><a href="https://www.nginx.com">NGINX</a></td>
    <td>Kubernetes Ingress Controller</td>
  </tr>
  <tr>
    <td><img width="32" src="https://cncf-branding.netlify.app/img/projects/prometheus/icon/color/prometheus-icon-color.svg"></td>
    <td><a href="https://prometheus.io">Prometheus</a></td>
    <td>Systems monitoring and alerting toolkit</td>
  </tr>
  <tr>
    <td><img width="32" src="https://avatars.githubusercontent.com/u/75713131?s=200&v=4"></td>
    <td><a href="https://rockylinux.org">Rocky Linux</a></td>
    <td>Base OS for Kubernetes nodes</td>
  </tr>
</table>

## Get Started

### Prerequisites

- Install the following apps on your env  
  - docker  
  - make  
  - vagrant  
  - virtualbox  
  - helm  
  - ansible
  
  
- VM spec (minimum recommendation)  
  ```
  # metal/Vagrantfile
  cpus = 4
  memory = "4192"
  disk_size = "10GB"
  ```
  
### Run  
Generate ssh pub/private keys  
```
ssh-keygen -f ~/.ssh/id_hyphen -t ecdsa -b 521
```  
Spin up the VM
```
VAGRANT_CWD=./metal vagrant up
```
Choose the network interface manually when asked (ex. 1 or 2 ...)
```
==> dev0: Importing base box 'rockylinux/8'...
==> dev0: Matching MAC address for NAT networking...
==> dev0: Checking if box 'rockylinux/8' version '4.0.0' is up to date...
==> dev0: Setting the name of the VM: metal_dev0_1644801016549_64462
==> dev0: Clearing any previously set network interfaces...
==> dev0: Available bridged network interfaces:
1) en0: Wi-Fi (AirPort)
2) en1: Thunderbolt 1
3) en2: Thunderbolt 2
4) bridge0
5) p2p0
6) awdl0
```  

Setup the cluster (this will take a while for all services up and running)
```
make dev
```

Check the cluster status
```
cd script
./get-status
```
Config DNS
```
- Use nip.io (suitable for a test environment) Or
- Change the DNS config in your router
https://www.noip.com/support/knowledgebase/how-to-configure-ddns-in-router/
```
Clean up
```
cd metal
vagrant destroy
or
rm -rf ~/VirtualBox\ VMs/* (for Mac)
```