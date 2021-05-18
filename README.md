# ez-kasten

```
./create_snapshot_class
helm repo add kasten https://charts.kasten.io  && helm repo update
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


#Insert data into the test database
CREATE DATABASE test;
\c test;
CREATE TABLE pets (name VARCHAR(20), owner VARCHAR(20), species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);
INSERT INTO pets VALUES ('Puffball','Diane','hamster','f','2010-03-30',NULL);
INSERT INTO pets VALUES ('Spike','Mike','pitbull','m','2011-04-28',NULL);
INSERT INTO pets VALUES ('Ashton','Varoon','German Sheperd','m','2014-06-15',NULL);
INSERT INTO pets VALUES ('Bear','Chris','Rottweiler','m','2013-10-10',NULL);
INSERT INTO pets VALUES ('Toby','Jenny','Golden Retriever','m','2019-03-19',NULL);

#Validate the data in the table PETS
test=# select * from pets;
   name   | owner  |     species      | sex |   birth    | death 
----------+--------+------------------+-----+------------+-------
 Puffball | Diane  | hamster          | f   | 2010-03-30 | 
 Spike    | Mike   | pitbull          | m   | 2011-04-28 | 
 Ashton   | Varoon | German Sheperd   | m   | 2014-06-15 | 
 Bear     | Chris  | Rottweiler       | m   | 2013-10-10 | 
 Toby     | Jenny  | Golden Retriever | m   | 2019-03-19 | 
(5 rows)

```
