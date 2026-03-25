pod created by kubelet without an api-server

in /etc/kubernetes/manifests

Create a static pod named static-busybox that uses the busybox image , run in the default namespace and the command sleep 1000

kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml

sudo find / -type f -name "config.yaml"

