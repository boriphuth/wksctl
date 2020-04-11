# wksctl
Deploy kubernetes via GitOps

```bash
vagrant up
vagrant status

for i in `seq 2212 10 2232`; do ssh -p $i vagrant@127.0.0.1 -i ~/.vagrant.d/insecure_private_key -o StrictHostKeyChecking=no "hostname && exit"; done

```

```bash
curl -LO https://github.com/weaveworks/wksctl/releases/download/0.8.1/wksctl-0.8.1-darwin-x86_64.tar.gz

tar xfz wksctl-0.8.1-darwin-x86_64.tar.gz
sudo chmod +x wksctl
sudo mv wksctl /usr/local/bin

wksctl init --git-url=https://github.com/sssd-dev/wksctl.git --git-branch=v1.0

```
curl https://releases.rancher.com/install-docker/19.03.sh | sh