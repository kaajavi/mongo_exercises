### This repo is for educational propouse
# ITS VILLADA
## Base de datos II

1 - Deploy docker

``docker-compose up -d``


2 - Copy mflix db to container
Now, we need copy mflix folder inside mongo db container for restore.
When you run docker compose, you can see the name of container, like [yourfolder]\_mongo\_[n]
In my case, _mongo2019\_mongo\_1_. You need call docker command, becouse with you can't 
use docker-compose for copy data inside conteiner. 

``docker cp mflix mongo2019_mongo_1:mflix/``

Now, you can restore database.

3 - Run restore

```bash
yourUserPath$ docker-compose exec mongo /bin/bash

root@id-container$ mongorestore --gzip --db mflix mflix/

```