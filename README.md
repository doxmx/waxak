# waxak

k8 bootstrap (kubeadm)

# TODO

## Node prep
- sshd - Disable passwordauth
- kube user
  - Create kube user
  - Add kube user to appropriate groups(sudo, wheel)
  - Create ssh pair key for kube user
  - Add ssh pub key to authorized keys for kube user


## K8 prep
- Install/config container runtime
  - docker.io
    - exec-opts
      /etc/docker/daemon.json
      ```
      {            
       "exec-opts": ["native.cgroupdriver=systemd"]
      } 
      ```
  - cri-o ?

- Import kubernetes gpg keys
  - apt.kubernetes.io/doc/apt-key.gpg
  - yum ?

- Enable repo
  - https://apt.kubernetes.io
  - yum ?

- Install packages
  - kubelet
  - kubeadm
  - kubectl

### Master
- init masternode
- copy kube configs to kube user
  ```
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  ```
- add completions to ~/.bashrc
  - echo 'source <(kubectl completion bash)' >> ~/.bashrc
  - echo 'source <(kubeadm completion bash)' >> ~/.bashrc
- Install a SDN
  - flannel 
    kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
  - calico 
    kubectl apply -f https://docs.projectcalico.org/v3.2/getting-started/kubernetes/installation/hosted/etcd.yaml
    kubectl apply -f https://docs.projectcalico.org/v3.2/getting-started/kubernetes/installation/rbac.yaml
    kubectl apply -f https://docs.projectcalico.org/v3.2/getting-started/kubernetes/installation/hosted/calico.yaml

### Nodes
  - Join node to master
    kubeadm join w.x.y.z:6443 --token 123456.1234567890 --discovery-token-ca-cert-hash sha256:01234567890abcd..


## Envs
- Create users for contexts
- Create contexts

## Tear Down
- Backup etcd (?)
- Remove nodes from the cluster

