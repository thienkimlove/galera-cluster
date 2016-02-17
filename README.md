# galera-cluster

# Usage

1. create node1 :

docker run -d --name node1 -h node1 thienkimlove/galera-cluster --wsrep-cluster-name=local-test --wsrep-cluster-address=gcomm://


2. Create node 2 :

docker run --detach=true --name node2 -h node2 --link node1:node1 thienkimlove/galera-cluster --wsrep-cluster-name=local-test --wsrep-cluster-address=gcomm://node1

3. Create node 3 : 

docker run --detach=true --name node3 -h node3 --link node1:node1 thienkimlove/galera-cluster --wsrep-cluster-name=local-test --wsrep-cluster-address=gcomm://node1


#setup mysql for each node :

docker exec -it node1 /bin/bash

mysql_secure_installation

set disallow remote to no.

GRANT ALL ON *.* to 'root'@'%' IDENTIFIED BY 'tieungao';
FLUSH PRIVILEGES;




#test
docker exec -ti node1 mysql -e 'show status like "wsrep_cluster_size"'

# Diffirent between Standard mysql and galera Cluster

http://galeracluster.com/documentation-webpages/limitations.html

#Read more 

http://planet.mysql.com/entry/?id=5989966
