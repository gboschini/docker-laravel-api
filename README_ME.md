## Development environment
### Docker Install

Install docker on your local machine: [Install Docker Engine](https://docs.docker.com/engine/installation/)



Append the following host to your /etc/hosts file
    
    127.0.0.1 www.thefamily.dev

Setup docker containers
    
    docker-compose build --no-cache

Install project dependencies

    docker-compose run web composer install

copy the settings file

    cp .env.dist .env

Build the database

    docker-compose run web php artisan migrate


## Run the application
Run the application, create the docker containers if needed

    docker-compose up

and access the api by browsing  <http://www.thefamily.dev>

Stop the application (also stop all docker containers) 
    
    docker-compose down
    
Access to the 'mydb' PG database with user 'user_write'

    docker-compose run web psql -h postgres platform tf_write
