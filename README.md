# wksctl
Deploy kubernetes via GitOps https://github.com/weaveworks/wksctl

## WKS and Vagrant
```bash
$ vagrant up
$ rm -rf $HOME/.ssh/known_hosts
$ for i in `seq 2212 10 2232`; do ssh -p $i vagrant@127.0.0.1 -i ~/.vagrant.d/insecure_private_key -o StrictHostKeyChecking=no "hostname && exit"; done

$ ssh -p 2222 vagrant@127.0.0.1 -i ~/.vagrant.d/insecure_private_key -o StrictHostKeyChecking=no "hostname && exit"

wksctl init --git-url=https://github.com/sssd-dev/wksctl.git --git-branch=v1.0
wksctl apply --git-url "https://github.com/sssd-dev/wksctl.git" --git-branch "develop"

$ wksctl apply --ssh-key=$HOME/.vagrant.d/insecure_private_key

$ wksctl kubeconfig --ssh-key=$HOME/.vagrant.d/insecure_private_key
$ wksctl kubeconfig --artifact-directory ../
$ export KUBECONFIG=../weavek8sops/example/kubeconfig
```

```bash
$ vagrant ssh kube-01
[vagrant@kube-01 ~]$  sudo -i
```
# It takes a few minutes for the controller to create the second node.
```bash
[root@kube-01 ~] kubectl get nodes
[root@kube-01 ~] for i in `seq 2 1 3`; do kubectl label node 'kube-0'$i node-role.kubernetes.io/worker=worker; done
```
NAME      STATUS   ROLES    AGE     VERSION
kube-01   Ready    master   8m8s    v1.13.3
kube-02   Ready    <none>   4m53s   v1.13.3

At any time, one can look at what the controller is doing:
```bash
[root@kube-01 ~] kubectl logs --tail 100 -f -n weavek8sops -l name=wks-controller
```