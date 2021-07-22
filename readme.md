## django in docker

## creating a docker container for django development
this is how i create my django base template inside docker

## pre requisite
_Follow the official installation guide_
- docker-engine [link](https://docs.docker.com/engine/install/ubuntu/)
- docker-compose [link](https://docs.docker.com/compose/install/)

## Get Started
- pull this repo
- open directory in terminal
- type
    ```
    docker-compose run web django-admin startproject <name-of-your-project> .
    ```
- this will first run the service named `web` defines in the `services` in `docker-compose.yml`
- as it has dependency on db, db service will also start.
- if command executed successfully a django project will be created. 
## Ownership of files
- in `linux` all files will be `root` owned, meaning cant modify without sudo command.
- type
    ```
    sudo chown -R $USER:$USER .
    ```
- this will make all `existing` files owner to local user, i.e. modifiable without root
- Creating app using `python manage.py <name-of-your-app>` will make that `app owned by root`, thus run the above command again to get going.
## Database Configuration
- this repos uses postgres as the default `db`
- change the default database of django in `settings.py` to 
    ```
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'postgres',
            'USER': 'postgres',
            'PASSWORD': 'postgres',
            'HOST': 'pgdb',
            'PORT': 5432,
        }
    }
    ```
- make sure the name, user and password of database matches with the data in `docker-compose.py`
## Django based commands
- to get access to the bash of docker type
    ```
    docker exec -it <container-id> bash
    ```
- run all django related command in this bash, e.g. `python manage.py makemigrations` or `python manage.py migrate` or `python manage.py createsuperuser`