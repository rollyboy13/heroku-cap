# Casting Flask App

The casting app improves the workflow in the movie industry by providing a tech stack that enables casting assistants, casting directors, and executive producers be on the same page about the status of movies and actors while controlling the rights of the involved parties to ensure the data regarding movies and actors are accurate.

Building this app calls upon the ability to model data and characteristics of that data, manage the data, implement the models in a database. Implementing this app allows for the use of an ORM to communicate with the database in a cleaner manner. Finally implementing this app calls on the ability to implement and test an API which exposes the data to the public to be manipulated by specific individuals according to their roles and permissions associated with those roles through authentication.

# Installing the app
## Install python 3.7 
Instructions for installing python 3.7 can be found at the official python documentation at https://docs.python.org

## Install the latest version of pip
pip is the python package management software
Instructions for the installation can be found at pypi.org

## Install virtualenv and create a virtual environment
A virtual environment helps isolate python applications so they run with the necessary dependencies without affecting other python applications
Visit https://virtualenv.pypa.io for instructions for installing virtualenv

run "virtualenv venv ." in the terminal to create a virtual environment in the current directory.
run "source venv/bin/activate" to activate the environment in UNIX systems


## Install other dependencies
Install the required dependencies by executing the following command in the terminal
"pip install -r requirements.txt"
or
"pip3 install -r requirements.txt" 

## Key dependencies
- Flask (https://flask.pocoo.org) is a microservices framework that provides the backend for the app

- SQLAlchemy (https://sqlalchemy.org) is the ORM used to interact with a postgres database

- Postgresql (https://postgresql.org) is the sql database dialect used for this app

- Flask-Migrate (https://flask-migrate.readthedocs.io) is the migration software used to manage the versions of the database

## Set up the third-party authentication
After setting up an Auth0 app and api
- add the auth domain as an environment variable with the key "AUTH0_DOMAIN"
- add the algorithm as an environment variable with the key "ALGORITHMS"
- add the api audience as an environment variable with the key "API_AUDIENCE"

Users must be set up in the appropriate Auth0 app

## Starting up the server
To run the server, execute:
"export FLASK_APP=app.py"
"export FLASK_ENV=development"
"flask run"


## Deployed web app link: 
https://casting-app-ru13.herokuapp.com/

##RBAC
The three roles as described in the intro are the casting assistant, casting director, executive producer roles. The permissions for each of these roles are described here.

-casting assistant: a user with this role can view the collections actors and movies as well as the details of individual actors and movies

-casting director: a user with this role has the permissions of the casting assistant. In addition, this user can add and remove an actor from the database as well as modify actors' and movies' data

-executive produce: a user with this role has the permissions of the casting director. In addition, this user can add and remove movies from the database.


##Endpoints

### GET:
'/actors'
- Returns a list of all the actors in the database

'/movies'
- Returns a list of all the movies in the database

'/actors/{id}'
- Returns a json representation of an actor with a specific id

'/movies/{id}'
- Returns a json representation of a movie with a specific id

### POST:
'/actors'
- Creates an actor in the database.
- json body must have the name, age and gender fields
- {"name": "name", "age": 22, "gender": "male"}

'/movies'
- Creates an movie in the database.
- json body must have the title and release_date fields
- {"title": "title", "release_date": "02-02-2020"}

### PATCH:
'/actors/{id}'
- Modifies an actor in the database.
- json body may have any of the name, age and gender fields
- {"name": "name", "gender": "male"}

'/movies/{id}'
- Modifies an movie in the database.
- json body may have any of the title and release_date fields
- {"title": "title", "release_date": "02-02-2020"}

### DELETE:
'/actors/{id}'
- Deletes an actor with the specified id from the database
'/movies/{id}'
-Deletes a movie with the specified id from the database


## Testing
To run tests, run with psql
dropdb {databasename}
createdb {databasename}
python test_app.py

Ensure that before running delete and patch test the id needs to be in the database for the test to be successful
To setup the tokens create the following environment variables
"CA_CRED" whose value is the token of a casting assistant user
"CD_CRED" whose value is the token of a casting director user
"EP_CRED" whose value is the token of a executive producer user

## USERS CREDENTIALS
token casting-assistant:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkdVcWc2Rnc2em5lWV9UZjVqTHJldiJ9.eyJpc3MiOiJodHRwczovL2ZzLXJvbGx5LmV1LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjEzMGY2YTY3ZjE5NDAwMTk5Y2M2MTgiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNTk1MTMwMzkzLCJleHAiOjE1OTUyMTY3OTMsImF6cCI6InZCTUQzWlczNkxwdWVUanA0V1o0eG10TndPQzdmNDdVIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyJdfQ.lpJ8q0ujkMib2BNPhmaL0y9_9j_edM1iBXtEw8KMC5uiFRrBSKGRlO3M3zrqg2XB8h3uwTFx0Te4yo5_Ut39wd_C-vJkDv56XmpNCoWpEEInL1cuIsG9ircuJRyMId_-pyXM_vAgLpLKU2_ofF52WG7wgwOX59zzVpVowdouuhEwKXGcy2L9DrRvZTmULV2TnxshYHcPuAiQONQs_0Hq_rZXrt_xVbLrHtiOBfXsrLymqdgat_paHZjr0WtLKT6K1mE190jZJeIAbi3HK51DCqWkBzRxfIpdZWLZ8Vm1vB8OOhcMahUNgOwFTsPuaTtFazuKMnEi9HVg6v2-V7CGOg

token casting-director:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkdVcWc2Rnc2em5lWV9UZjVqTHJldiJ9.eyJpc3MiOiJodHRwczovL2ZzLXJvbGx5LmV1LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjEzMTAwZjhhMGVkODAwMTMzMTcyMjUiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNTk1MTMwNDkwLCJleHAiOjE1OTUyMTY4OTAsImF6cCI6InZCTUQzWlczNkxwdWVUanA0V1o0eG10TndPQzdmNDdVIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6YWN0b3IiLCJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyIsInBhdGNoOmFjdG9yIiwicGF0Y2g6IG1vdmllIiwicG9zdDphY3RvciJdfQ.TjKLmcLJPjLgCjgDkzyVYqG3UhLJGkRmT8PW9tUr9xZnhSUoeNJ965dnHD3y5E3enQ3N2FHTgareVVXNVsKDTa3YUgeUlDfaZ6zYqVl0kvmTzZJhpLsN95QMN4rmR8ScM1ERrpDHPoNAP8C9z0ngJFu_14XltKeWr4gq4JrcLyIq4YM0yGXbaWfa1gJLxhDPbmnRN8cJPVZk3rDegqoEqws8tHcQQ6BLJvmBN7WOdkHFZskRwl0w1jRPIQL836apNCiDMW8zudlGNzcQqac8cYejfVVtEVxrhqoNAC87WRS5SvbOWagTiAQUqzR3IHc9_fsken53qtanUNPYnPCofQ

token executive-producter:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkdVcWc2Rnc2em5lWV9UZjVqTHJldiJ9.eyJpc3MiOiJodHRwczovL2ZzLXJvbGx5LmV1LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjEzMTA4YzhhMGVkODAwMTMzMTcyNWQiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNTk1MTMwNTc0LCJleHAiOjE1OTUyMTY5NzQsImF6cCI6InZCTUQzWlczNkxwdWVUanA0V1o0eG10TndPQzdmNDdVIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6YWN0b3IiLCJkZWxldGU6bW92aWUiLCJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyIsInBhdGNoOmFjdG9yIiwicGF0Y2g6IG1vdmllIiwicG9zdDphY3RvciIsInBvc3Q6bW92aWUiXX0.tyTe6SrLk0q7nXFQz5z7XBwfCyrn_ACxoc1WqCWUilAtCgXasYlYwiflXBtJQCn850tsDxB_sGLLPmJn7SauuEQt1ffzA9v3q-pgQXS7Q5JKV0RSuq4SUlAaJaPbaDX79m4CaAP5OtLdSba_sKftyPYJJPM0Qf3MyN152vlzcV7KZ1AEyZhBKQzOytoClhylcDWbWjnyv5bu5liyLDxqIDrBGjCWoani5qOWEO27MXFzZfFaKqzmDvggEDzvLQt50t0dSqOjR0oEYT1kbNcldhLILxplY2K4unx45DDb9qz5Jy_m89RI3hNEmY4FP5an_bPqxFVIrHc7oYejFWkZLA
