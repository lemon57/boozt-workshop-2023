# boozt-workshop-2023 
# DB indexing

# Set up work envoironment for the workshop with mysql base docker container and test database
1. Create working directory on your laptop, for example: `workshop-indexing`
2. Download dump of the test database from [goodle drive](https://drive.google.com/drive/folders/1bh1RH_43jPEBn6nSGAYvlnT6apVNHtPN?usp=share_link) and put it inside working derectory `workshop-indexing` on your laptop
2. Git clone this repo (docker-compose.yml): `git clone git@github.com:lemon57/boozt-workshop-2023.git`
3. Start docker container, inside your working directory run: `docker compose up -d`
4. Check that the docker container is up and we have connection to DB: 
    `docker compose exec -it mysql mysql -u root --password=index`
    you should get mysql prompt       
5. We should have our test database: `index_test`, check what database you have by this command, run inside mysql prompt this command: 
    `show databases;`
6. Take the name of the container, run this command to see the list of the containers: `docker ps`
  In my case I have `index-yes-mysql-1` name of the container.
7. If database exist run import DB dump into docker container:
`cat backup_index0519.sql | docker exec -i index-yes-mysql-1 /usr/bin/mysql -u root --password=index index_test`

Now you should have ready test DB inside our docker container. Inside `index_test` DB you should have two tables: `customers` and `orders` with some dummy data. 

Time to start our workshop :)
