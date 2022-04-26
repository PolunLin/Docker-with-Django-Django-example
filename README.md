# Docker with Django example
| This repo is for practicing run django service with PostgreSQL in docker container
## How to Create

### 1. Create a docker file 

```bash
FROM python:3
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/
```

### 2. Create requirements.txt file

```bash
Django>=2.0,<3.0
psycopg2>=2.7,<3.0
```

### 3. create docker-compose.yml

```bash
version: "3"
services:

  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: 'postgres'

  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
```

## run the application

```bash
docker-compose run web django-admin startproject django_example .
```
And we will create 


```
    Django with docker
    │  docker-compose.yml
    │  Dockerfile
    │  manage.py
    │  READ.md
    │  requirements.txt
    │
    └─django_example
        │  settings.py
        │  urls.py
        │  wsgi.py
        │  __init__.py
```
If your OS is linux, modify the file permission

```
$ sudo chown -R $USER:$USER .
```

## Set DB connection information

```bash
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
        'PASSWORD': 'postgres',
    }
}
```
## Run docker-compose up
```bash
docker-compose up
## docker-compose run web python manage.py syncdb
```
