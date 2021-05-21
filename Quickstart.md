kubectl create configmap -n kube-system kubevirt-config --from-literal debug.useEmulation=true
export KUBEVIRT_VERSION=$(curl -s https://api.github.com/repos/kubevirt/kubevirt/releases|grep tag_name|sort -V | tail -1 | awk -F':' '{print $2}' | sed 's/,//' | xargs)
echo $KUBEVIRT_VERSION
kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-operator.yaml
kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-cr.yaml
kubectl get pods -n kubevirt
virtctl is a client utility to provide some more convenient ways to interact with the VM:
wget -O virtctl https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/virtctl-${KUBEVIRT_VERSION}-linux-amd64
chmod +x virtctl
kubectl apply -f https://raw.githubusercontent.com/kubevirt/demo/master/manifests/vm.yaml

kubectl get vms
./virtctl start testvm
kubectl get vmis
