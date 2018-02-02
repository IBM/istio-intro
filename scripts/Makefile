SHELL := /bin/bash
REGISTRY := cmluciano/istio-intro
VERSION ?= $(shell git describe --tags --always --dirty)

minikube:
	minikube start \
	--extra-config=controller-manager.ClusterSigningCertFile="/var/lib/localkube/certs/ca.crt" \
	--extra-config=controller-manager.ClusterSigningKeyFile="/var/lib/localkube/certs/ca.key" \
	--extra-config=apiserver.Admission.PluginNames=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota \
	--kubernetes-version=v1.9.0

download:
	curl -L https://git.io/getLatestIstio | sh -
	cp -r ./istio-0.5.0/* .

setup:
	kubectl apply -f ./install/kubernetes/istio.yaml

watch:
	watch -n3 kubectl get pods --all-namespaces

create-cert:
	./install/kubernetes/webhook-create-signed-cert.sh \
	    --service istio-sidecar-injector \
	    --namespace istio-system \
	    --secret sidecar-injector-certs

check-cert:
	kubectl -n istio-system get certificatesigningrequest

deploy-configmap:
	kubectl apply -f install/kubernetes/istio-sidecar-injector-configmap-release.yaml

check-configmap:
	kubectl -n istio-system get cm istio-inject

create-cabundle:
	cat install/kubernetes/istio-sidecar-injector.yaml | \
	     ./install/kubernetes/webhook-patch-ca-bundle.sh > \
	     ./install/kubernetes/istio-sidecar-injector-with-ca-bundle.yaml

deploy-injector:
	kubectl apply -f install/kubernetes/istio-sidecar-injector-with-ca-bundle.yaml

check-injector:
	kubectl -n istio-system get deployment -listio=sidecar-injector

label-default:
	kubectl label namespace default istio-injection=enabled
	kubectl get namespace -L istio-injection

deploy-sleep:
	kubectl create -f samples/sleep/sleep.yaml
