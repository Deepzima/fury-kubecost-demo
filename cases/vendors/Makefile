MINIKUBE_CLUSTER_NAME=zimernetes-one
MINIKUBE_DRIVER=qemu
K8S_VERSION=v1.26.0
RUNTIME=containerd
NODES=1
CPU=6
MEMORY=12000
CNI_TYPE=calico
SETUP=minikube-stand
CLUSTER1_IP=192.168.64.101
CLUSTER2_IP=192.168.64.102
MINIKUBE_DRIVER=quem

.PHONY: vendors
vendors:
	furyctl vendor -H

.PHONY: kubecost
	helm template cost-analyzer stable/cost-analyzer  --output-dir  kubecost/kubecost-manifests/helm-manifests

.PHONY: delete
delete:
	minikube delete --profile $(MINIKUBE_CLUSTER_NAME)
	minikube cache delete

.PHONY: start
start:
	minikube start --profile $(MINIKUBE_CLUSTER_NAME)

.PHONY: stop
stop:
	minikube stop --profile $(MINIKUBE_CLUSTER_NAME) 

.PHONY: setup
setup: minikube-stand

.PHONY: minikube-stand
minikube-stand:
	minikube start \
		--profile $(MINIKUBE_CLUSTER_NAME) \
        --kubernetes-version $(K8S_VERSION) \
        --driver $(MINIKUBE_DRIVER) \
		--container-runtime $(RUNTIME) \
        --memory $(MEMORY) \
        --cpus $(CPU) \
		--cni $(CNI_TYPE) \
        --nodes $(1) \
        --embed-certs 