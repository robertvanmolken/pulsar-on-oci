# Pre-requirements Pulsar on OCI

## OIC: Provision a new OKE cluster

## Local: download and install OCI CLI
```bash
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
```

## Local: Run OCI setup config (need user + tenant OCID)
```bash 
oci setup config  
```
  
## OCI: Upload public key to user

## Local: Check kube configuration
```bash
export KUBECONFIG=$HOME/.kube/configOCI
kubectl config view
```

## Local: Clone pulsar repository
```bash
git clone https://github.com/apache/pulsar
cd pulsar
```

## Local: Install helm v3
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh 
```
  
## Local: Add streamnative helm charts
```bash
helm repo add streamnative https://charts.streamnative.io
```

## Local: Install local storage provisioner (optional)
```bash
helm install pulsar-storage-provisioner streamnative/local-storage-provisioner
```

## Local: Install cert manager (optional)
```bash 
./scripts/cert-manager/install-cert-manager.sh
```
  
## Local: Prepare helm release of pulsar
```bash
./scripts/pulsar/prepare_helm_release.sh \
  -n pulsar \
  -k pulsar-mini \
  --control-center-admin pulsar \
  --control-center-password pulsar \
  -c
```

## Local: Helm install pulsar using minikube example values
```bash
cat examples/values-minikube.yaml
helm install \
  --values examples/values-minikube.yaml \
  pulsar-mini pulsar
```
	
## Local: Check if pulsar is installed
```bash
kubectl get service -n pulsar
```
  
## Local: Get external IP addresses of manager, broker and grafana
```bash
kubectl get service -n pulsar
```

## View Pulsar Consoles

* Login to Pulsar Admin UI
  > [http://service-ip:9527/#/login](http://193.122.14.136:9527/#/login)
  
* Login to Grafana UI
  > [http://service-ip:3000/login](http://130.61.14.119:3000/login)
  
## Next

[Getting started with Pulsar](01_getting-started.md)
