
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
<img width="1229" alt="Screenshot 2021-05-27 at 10 11 43" src="https://user-images.githubusercontent.com/82048393/119799695-3b2bc300-bed4-11eb-9a56-3c947728b0de.png">

