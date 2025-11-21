# Lab 13 

## Question 1: How would you rollback to a previous version of the deployment?

**Answer:**
```bash
# View rollout history
kubectl rollout history deployment/notes-deployment -n notes-app

# Rollback to previous version
kubectl rollout undo deployment/notes-deployment -n notes-app

# Rollback to specific revision
kubectl rollout undo deployment/notes-deployment -n notes-app --to-revision=1
```

## Question 2: How would you scale the deployment to 3 replicas?

**Answer:**
```bash
# Option 1: Using kubectl scale
kubectl scale deployment notes-deployment --replicas=3 -n notes-app

# Option 2: Edit the deployment
kubectl edit deployment notes-deployment -n notes-app
# Change replicas: 2 to replicas: 3
```

## Question 3: How would you apply a Resource Quota to the namespace?

**Answer:**
Create `resource-quota.yaml`:
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: notes-quota
  namespace: notes-app
spec:
  hard:
    requests.cpu: "2"
    requests.memory: 2Gi
    limits.cpu: "4"
    limits.memory: 4Gi
```

Apply it:
```bash
kubectl apply -f resource-quota.yaml
```
