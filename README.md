# dataset.EntrezGene

### Start MySQL on Docker 

```bash 
docker pull jhsong/mysql 
docker run -p 33060:3306 --name entrez_gene -e MYSQL_ROOT_PASSWORD='docker' -d jhsong/mysql
```

### Option 1. Database restoring from the author  

http://barc.wi.mit.edu/entrez_gene/

```bash 
# step 1. download data
perl download_parse_entrezgene.pl
# step 2. createdb entrez_gene
mysql < tables_for_entrezgene.sql
# step 3. dataset restore 
sh -c load_entrezgene.sh
```

### Option 2. Database restoring from preprocessed database dump 

```bash 
# step 1. create database
echo 'create database entrez_gene' | docker exec -i entrez_gene mysql -uroot --password=docker
# step 2. restore database 
cat dump-entrez_gene.sql | docker exec -i entrez_gene mysql -uroot --password=docker
```

