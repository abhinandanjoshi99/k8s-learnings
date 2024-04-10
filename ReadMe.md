<!-- GETTING STARTED -->
## Getting Started

In this repo, I will be sharing all my learning with k8s(AKS,EKS and GKE).

### How to get rid of a k8s namespace which is stuck in "terminating" state?

This happens if a Kubernetes API extension is not available, and the resources that are managed by the extension cannot be deleted. 
* Command to get rid of the namespace
  ```sh
  NS=kubectl get ns |grep Terminating | awk 'NR==1 {print $1}' && kubectl get namespace "$NS" -o json   | tr -d "\n" | sed "s/\"finalizers\": \[[^]]\+\]/\"finalizers\": []/"   | kubectl replace --raw /api/v1/namespaces/$NS/finalize -f -
  ```
