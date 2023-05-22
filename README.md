# boozt-workshop-2023 - DB indexing :card-index-dividers:

### Useful info:
- Our workshop slack channel is `pt-conf-2023-workshop-db-index`.   
  Feel free ask any questions there in case you are remote during workshop or you have any issues with setting up the work envoironment. 

### Set up work envoironment for the workshop   
Using mysql-base docker container and dummy test database:  
1. On your local machine, inside home directory, create working directory for example:   
  `mkdir workshop-indexing`  
  `cd workshop-indexing`   
2. Git clone this repo (docker-compose.yml and some initial sql script for DB):  
  `git clone git@github.com:lemon57/boozt-workshop-2023.git`   
  `cd boozt-workshop-2023`   
3. Download dump of the test database from  
  [goodle drive](https://drive.google.com/drive/folders/1bh1RH_43jPEBn6nSGAYvlnT6apVNHtPN?usp=share_link)   
  Download only this sql file `backup_index0522.sql`     
  Move it inside `~/workshop-indexing/boozt-workshop-2023` on your local machine  
4. Start docker container:
  Go to `~/workshop-indexing/boozt-workshop-2023`  
  Run `docker compose up -d`  
  Your docker container based on mysql-base image should be up now.  
  To check that, run:  
  `docker ps`  
  You should see the docker container with the name `boozt-workshop-2023-mysql-1`.  
5. Check connection to your test DB inside the container:
  Inside this directory `~/workshop-indexing/boozt-workshop-2023`   
  run `docker compose exec -it mysql mysql -u root --password=index`  
  You should get mysql prompt:  
  `mysql>`  
  Inside this mysql prompt run `show databases;`, you should see `index_test` DB.  
  Type `exit;`. You should be now inside `~/workshop-indexing/boozt-workshop-2023` directory again.        
6. Get the name of your container:  
  Run `docker ps`, the name should be `boozt-workshop-2023-mysql-1`.  
7. Your docker container is up and `index_test` DB exist,    
  then import prepared DB dump data (downloaded sql file) inside this DB.  
  Inside `~/workshop-indexing/boozt-workshop-2023`  
  Run:   
  `cat backup_index0522.sql | docker exec -i boozt-workshop-2023-mysql-1 /usr/bin/mysql -u root --password=index index_test`

  Now your test DB inside the docker container is ready.   
  `index_test` DB should have two tables: `customers` and `orders` with some dummy data. 

8. You should also have one of the DB management tool to connect to the DB and run queries.
  - Sequel ACE,
  - DBeaver,
  - or any other

9. Using your DB management tool connect to your test DB.    
  Connection specs:
  - host: 127.0.0.1
  - username: root
  - password: index
  - database: index_test     
  Select `index_test` DB and check that you have two tables `orders` and `customers` with data.    

Now your work envoironment for the workshop is ready.    
If you have any questions just ask in the channel `pt-conf-2023-workshop-db-index`.
