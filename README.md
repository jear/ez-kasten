# ez-kasten

```
./create_snapshot_class
helm repo add kasten https://charts.kasten.io --force-update && helm repo update
kubectl create ns kasten-io
kubectl annotate volumesnapshotclass mapr-snapshotclass k10.kasten.io/is-snapshot-class=true

curl -s https://docs.kasten.io/tools/k10_primer.sh | bash

curl -s https://docs.kasten.io/tools/k10_primer.sh | bash /dev/stdin -c "storage csi-checker -s hcp-mapr-cluster --runAsUser=1000"
```
