# Python Feedbacks App (Django)
The Feedbacks project collects user feedback on works. The works are divided into categories: "Books", "Films", "Music".
The
list of categories (Category) can be expanded via Admin interface.

Using SQLite as DB, backend based on View-sets approach.
JWT-token for authorization.
DRF for permissions setup

Roles:

* Anonymous
    * can view descriptions of works, read reviews and comments
* User (authenticated)
    * can set text reviews
    * can set rate from 1 to 10. Average rate is based on all reviews set. Can leave 1 rate per work
    * can leave comments to reviews
* Moderator
    * same rights as an Authenticated User
    * can delete and edit any reviews and comments
* Administrator
    * same rights as Moderator user
    * can add works, categories and genres
    * can set roles
* Django superuser
    * same as administrator but cannot be set to another role unlike usual admin

Register process:

* User sends a request with the email parameter to /auth/email/.
* App sends an email with a confirmation code (confirmation_code) to the email address.
* User sends a request with the parameters email and confirmation_code to /auth/token/, in response to the request, he
  receives a token (JWT token).
* Optionally, user sends a PATCH request to /users/me/ and fills in the fields in his profile (the description of the
  fields is in the documentation). Full API Documentation (redoc.yaml)

### Built With

* [![Python][Python.io]][Python-url]
* [![Django][Django.io]][Django-url]
* [![SqlLite][SqlLite.io]][SqlLite-url]
* [![Nginx][Nginx.io]][Nginx-url]
* [![Unicorn][Unicorn.io]][Unicorn-url]
* [![Docker][Docker.io]][Docker-url]


## Pre-installations

#### Clone the repo:

```sh
git clone https://github.com/AdeleDev/feedbacks_python_app.git
```

#### Set .env file:

```
Take infra/.env.example as initial file
Rename ".env.example" to ".env"
Set necessary values in the file
```

## Usage

#### Copy files
```
Copy the docker-compose.yaml and nginx/default.conf files from project to the server to home/<your_username>/docker-compose.yaml and home/<your_username>/nginx/default.conf respectively
```

#### Start docker-compose:

```sh
cd yamdb_final/infra
```

```sh
docker compose up
```

#### Do migrations:

```sh
docker-compose exec web python manage.py makemigrations --noinput  
docker-compose exec web python manage.py migrate --noinput
```

#### Create superuser:

```sh
docker-compose exec web python manage.py createsuperuser
```

#### Add db initial data:

```sh
docker-compose exec web python manage.py loaddata fixtures.json
```

#### Open project:

Navigate to http://localhost:8000/

## API example requests:

API documentation:

```
http://127.0.0.1:8000/redoc/
```

Get JWT-token request:

```
http://127.0.0.1:8000/api/v1/jwt/create
```

Get genres request:

```
http://127.0.0.1:8000/api/v1/genres/
```

Get titles:

```
http://127.0.0.1:8000/api/v1/titles/
```

<!-- MARKDOWN LINKS & IMAGES -->

[Python.io]: https://img.shields.io/badge/-Python-yellow?style=for-the-badge&logo=python

[Python-url]: https://www.python.org/

[Django.io]: https://img.shields.io/badge/-Django-darkgreen?style=for-the-badge&logo=django

[Django-url]: https://www.djangoproject.com/

[SqlLite.io]: https://img.shields.io/badge/-SQLite-blue?style=for-the-badge&logo=sqlite

[SqlLite-url]: https://www.sqlite.org/index.html

[Docker.io]: https://img.shields.io/badge/-Docker-lightblue?style=for-the-badge&logo=docker

[Docker-url]: https://docs.docker.com/

[Nginx.io]: https://img.shields.io/badge/-Nginx-lightgreen?style=for-the-badge&logo=nginx

[Nginx-url]: https://docs.docker.com/

[Unicorn.io]: https://img.shields.io/badge/-Gunicorn-white?style=for-the-badge&logo=gunicorn

[Unicorn-url]: https://docs.docker.com/
