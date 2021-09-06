# deploy-postgres

## Método 1:
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
export POSTGRES_PASSWORD=$(kubectl get secret --namespace postgres postgres-postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)
echo $POSTGRES_PASSWORD
kubectl run postgres-postgresql-client --rm --tty -i --restart='Never' --namespace postgres --image docker.io/bitnami/postgresql:11.13.0-debian-10-r12 --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgres-postgresql -U postgres -d postgres -p 5432
```

## Método 2:
```bash
git clone https://github.com/Mundo-Dev0ps/deploy-postgres
cd deploy-postgres
kubectl apply -f all-in-one.yaml
POD=`kubectl get pods -n postgres -l app=postgres -o wide | grep -v NAME | awk '{print $1}'`
echo $POD
kubectl exec -n postgres -it $POD -- psql -U postgres
```
