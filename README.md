# Kubeflow on Minikube

**Warning**: Kubeflow manifest doesn't work with [latest](https://kubernetes.io/releases/) (v1.23.3) version. Please use the following commands to use the older Kubernetes version.

* Kubernetes version: `1.20.14`
* [Kustomize version](https://github.com/kubernetes-sigs/kustomize/releases/tag/kustomize%2Fv3.2.3): `3.2.3`
* [Kubeflow version](https://github.com/kubeflow/manifests/archive/refs/tags/v1.4.1.zip): `1.4.1`

## Prepare the Minikube

```
minikube start --cpus 6 --memory 10240 --disk-size 40GB --vm=true --kubernetes-version=v1.20.14

minikube addons enable metrics-server
```

## Install Kubeflow to minikube

**Warning**: Please check your Kubernetes context. Your `kubectl` context must be `minikube`.

```
while ! ./kustomize build example | kubectl apply -f -; do echo "Retrying to apply resources"; sleep 10; done
```

## Login to Kubeflow

**Info**: Please wait until Kubeflow is ready on your minikube. It takes 20-30 minutes depending on your computer power. Please use the following command to check pods.

```
kubectl get pods -n kubeflow --watch
```

Please use the following command to forward the pod's port to your local machine.

```
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80
```

Open the Kubeflow by http://localhost:8080/

* Email: `user@example.com`
* Password: `12341234`

For more information, please look to [Kubeflow manifests](https://github.com/kubeflow/manifests) repository.
