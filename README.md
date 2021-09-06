# deploy-postgres

## Método 2:
```bash
git clone https://github.com/Mundo-Dev0ps/deploy-postgres
cd deploy-postgres
kubectl apply -f all-in-one.yaml
POD=`kubectl get pods -n postgres -l app=postgres -o wide | grep -v NAME | awk '{print $1}'`
echo $POD
kubectl exec -n postgres -it $POD -- psql -U postgres
```
