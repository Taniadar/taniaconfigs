### Per a iniciar el servei galera: https://www.digitalocean.com/community/tutorials/how-to-configure-a-galera-cluster-with-mariadb-10-1-on-ubuntu-16-04-servers

Apagar servei mysqld
      
     systemctl stop mysqld

Al primer node executem

     galera_new_cluster

Per a veure els nodes registrats:

     mysql -u root -p -e "SHOW STATUS LIKE 'wsrep_cluster_size'"

Arranquem servei dels altres dos nodes:

	 systemctl start mysql
	 mysql -u root -p -e "SHOW STATUS LIKE 'wsrep_cluster_size'" ( a mesura que arrenca el servei han d'apareixer els respectius nodes actius).

Quan peti el cluster:

     /var/lib/mysql/grastate.dat

#### Trobar el node segur per a ser el primer en ser arrencat
    $ sudo cat grastate.dat
    # GALERA saved state
    version: 2.1
    uuid:    839f24ed-db82-11e8-a132-4379428c7fd4
    seqno:   -1
    safe_to_bootstrap: 0
    safe_to_bootstrap ha de ser 1!

Llavors en aquell node executar:
# galera_new_cluster

Un cop iniciat el servei mysql en el primer node, aixecar el servei a la resta.