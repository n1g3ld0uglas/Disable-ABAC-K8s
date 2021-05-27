
# Disable-ABAC-K8s

ABAC (Attribute-Based Access Control) is the authorization decision based on a subject's attributes, such as labels or properties.
Kubernetes' ABAC (Attribute Based Access Control) has been superseded by RBAC since release 1.6, and should not be enabled on the API server.

An attribute-based rule checks the below user attributes to decide whether a user is able to perform a task.
```
user.id='1234',user.project="project",user.status="active"
```


Here is how we would disable it in GKE:

```
gcloud container clusters update nigel-gke-cluster --zone europe-west2-a --no-enable-legacy-authorization
```
<img width="1229" alt="Screenshot 2021-05-27 at 10 11 43" src="https://user-images.githubusercontent.com/82048393/119803085-08cf9500-bed7-11eb-8caa-c83cb43adaa9.png">


In this case of AKS, it recommends creating the AKS cluster with managed Azure AD integration to use their version of Azure RBAC for Kubernetes Authorization:

```
az aks create --resource-group nigelResourceGroup --name nigelAKSCluster --node-vm-size Standard_B2ms --node-count 3 --zones 1 2 3 --network-plugin azure --enable-aad --enable-azure-rbac
```

With the Azure AD feature flag, it will throw the below error:
<img width="1117" alt="Screenshot 2021-05-27 at 10 31 23" src="https://user-images.githubusercontent.com/82048393/119802752-bbebbe80-bed6-11eb-84c0-77bc571ccfec.png">

Otherwise, you can add Azure RBAC for Kubernetes Authorization into an existing AKS cluster, using the az aks update command with the flag enable-azure-rbac:

```
az aks update -g nigelResourceGroup -n nigelAKSCluster --enable-azure-rbac
```

