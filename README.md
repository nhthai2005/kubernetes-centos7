# The following example starts a Redis container and configures it to always restart unless it is explicitly stopped or Docker is restarted.

$ docker run -d --restart unless-stopped redis


# Install kubectl on Linux

## Download the latest release with the command:

curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
## To download a specific version, replace the $(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt) portion of the command with the specific version.

## For example, to download version v1.18.0 on Linux, type:

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl
## Make the kubectl binary executable.

chmod +x ./kubectl
## Move the binary in to your PATH.

sudo mv ./kubectl /usr/local/bin/kubectl
## Test to ensure the version you installed is up-to-date:

kubectl version --client

# Run K9S in docker
### docker run --rm -it -v ~/.kube/config-mycluster:/root/.kube/config quay.io/derailed/k9s

mkdir ~/.kube/
scp  root@172.16.10.100:/etc/kubernetes/admin.conf ~/.kube/config-mycluster
docker run --rm -it -v ~/.kube/config-mycluster:/root/.kube/config quay.io/derailed/k9s

## Kubectl Dashboard, port 8001 --> proxy
docker run --rm -it -p 8001:8001 -v /home/docker/exams:/root/exams -v ~/.kube/config-mycluster:/root/.kube/config -v /home/docker/dashboard:/root/dashboard nhthai2005/ubuntu:kubectl


## Login https://172.16.10.100:31000 with token
## Tiếp theo chạy lệnh sau để lấy Token

kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

kubectl api-resources