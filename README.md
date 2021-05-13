# ez-kasten

```
./create_snapshot_class
helm repo add kasten https://charts.kasten.io --force-update && helm repo update
kubectl create ns kasten-io
kubectl annotate volumesnapshotclass mapr-snapshotclass k10.kasten.io/is-snapshot-class=true

curl -s https://docs.kasten.io/tools/k10_primer.sh | bash

curl -s https://docs.kasten.io/tools/k10_primer.sh | bash /dev/stdin -c "storage csi-checker -s hcp-mapr-cluster --runAsUser=1000"

# Install K10
helm install k10 kasten/k10 --namespace=kasten-io


# Test
helm repo add bitnami https://charts.bitnami.com/bitnami  && helm repo update
kubectl create ns postgresql
helm install postgresql bitnami/postgresql --namespace=postgresql --set volumePermissions.enabled=true

export POSTGRES_PASSWORD=$(kubectl get secret --namespace postgresql postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)

kubectl run postgresql-client --rm --tty -i --restart='Never' \
          --namespace postgresql \
          --image docker.io/bitnami/postgresql:11.11.0-debian-10-r50 \
          --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgresql \
          -U postgres -d postgres -p 5432

```
