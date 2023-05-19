# boozt-workshop-2023 - DB indexing

### Useful info:
- Our workshop slack channel is `pt-conf-2023-workshop-db-index`.
  Feel free ask any question there in case you are remote. 

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
  It should be inside `~/workshop-indexing/boozt-workshop-2023` on your local machine
4. Start docker container:
  `pwd` => `~/workshop-indexing/boozt-workshop-2023`
  Run `docker compose up -d`
  Your docker container on mysql-base image should be up now.
  To check that, run:
  `docker ps`
  YOu should see the docker container with name `boozt-workshop-2023-mysql-1`.
5. Check connection to our test DB on the container:
  From the same place run `docker compose exec -it mysql mysql -u root --password=index`
  You should get mysql prompt:
  `mysql>`
  Inside this mysql prompt run `show databases;`, you should see `index_test` DB.
  Type `exit;`. Yuo should be now inside `~/workshop-indexing/boozt-workshop-2023` directory.       
6. Get the name of your container:
  Run `docker ps`, the name should be `boozt-workshop-2023-mysql-1`.
7. Our docker container is up and `index_test` DB exist, then
  run import our DB dump data into the docker container.
  Inside `~/workshop-indexing/boozt-workshop-2023`
  Run:
  `cat backup_index0519.sql | docker exec -i boozt-workshop-2023-mysql-1 /usr/bin/mysql -u root --password=index index_test`

Now our test DB inside our docker container is ready. 
`index_test` DB should have two tables: `customers` and `orders` with some dummy data. 

Time to start our workshop :rocket:
