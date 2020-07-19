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
- "export FLASK_APP=app.py"
- "export FLASK_ENV=development"
- "flask run"


## Deployed web app link: 
https://casting-app-ru13.herokuapp.com/

## RBAC
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
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkdVcWc2Rnc2em5lWV9UZjVqTHJldiJ9.eyJpc3MiOiJodHRwczovL2ZzLXJvbGx5LmV1LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjEzMGY2YTY3ZjE5NDAwMTk5Y2M2MTgiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNTk1MTg3MTE4LCJleHAiOjE1OTUyNzM1MTgsImF6cCI6InZCTUQzWlczNkxwdWVUanA0V1o0eG10TndPQzdmNDdVIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyJdfQ.hRlZzu2cQHLJnOnjuf_4JaQKno6qwhPT6xZGRKYZ104pZtpiELMGqqVJdmcxBSOAn26IDhSfWTdnu3HTiSTPKbAl1zk3b0ziycf_n2qYywkPt6vLxW_zUQfVuBWh_3UxTlM5R8vATvi4UX-pzqdrTMWetdhu5wD-XLaqqOMgLnQY3pJ_zrq7KlhTpA-yuVQEVYm8O6PKOC7IFwrMl3qNRnBlyoY1CqWanRBTzw2gkNRTzGlVjzSPMvP8LD2nWqtCL4gMoRogNROAyCqgpbMSDMJRyUL2jkR0-u_Z1z9IjrS9h_E8xFw1NpePuqNLoymamyaO1exxem1ANjSp6FpvQA

token casting-director:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkdVcWc2Rnc2em5lWV9UZjVqTHJldiJ9.eyJpc3MiOiJodHRwczovL2ZzLXJvbGx5LmV1LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjEzMTAwZjhhMGVkODAwMTMzMTcyMjUiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNTk1MTg3MDQ0LCJleHAiOjE1OTUyNzM0NDQsImF6cCI6InZCTUQzWlczNkxwdWVUanA0V1o0eG10TndPQzdmNDdVIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6YWN0b3IiLCJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyIsInBhdGNoOmFjdG9yIiwicGF0Y2g6IG1vdmllIiwicG9zdDphY3RvciJdfQ.hQSuYog51NwQH5h_b4cy6urCi0a0FZiJEgI4YM-UorGaRvgMwAZ3w14rkwu6qQHEfClEn3adpdXWwtfKgENpeAQ8N-qxvksvi13M8OKeXYbtE5u3ItUfdqAjWV_E7FBGgkqEv6Ri5oH-2MZxtd28Qbk5CgpFNXgWisbjDx0aWMwbnuCPCK-QN-GaKvXMgqMUsdJ-sEmXVTR22tXx6G4nqct_uIx_j_qUJvjdLug0gzFjfLb_XbPTLnXRCZlLRoJAtLI0NLSWJrnuU39YwAODVBK2wz0QaiOgEitSQl5U7Qq2zQ1ek23sMfMaPDQC-iC68NuVac05gD6_qkIAaEiBMw

token executive-producter:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IkdVcWc2Rnc2em5lWV9UZjVqTHJldiJ9.eyJpc3MiOiJodHRwczovL2ZzLXJvbGx5LmV1LmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw1ZjEzMTA4YzhhMGVkODAwMTMzMTcyNWQiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNTk1MTg1OTYzLCJleHAiOjE1OTUyNzIzNjMsImF6cCI6InZCTUQzWlczNkxwdWVUanA0V1o0eG10TndPQzdmNDdVIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6YWN0b3IiLCJkZWxldGU6bW92aWUiLCJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyIsInBhdGNoOmFjdG9yIiwicGF0Y2g6IG1vdmllIiwicG9zdDphY3RvciIsInBvc3Q6bW92aWUiXX0.FM_dGSTiVJXuM8GnmnUxa8AoUPI2S4ezrG7KdDgTzYdUtCmF4fYqrtqvVAIvCTFbpVnyHH8HF3Y62qwAAEh0fIfhDKwOyFhs31bAWpEg5I6yma-YQg3vgzk00cTUVApUoMYRplR5DO4Tr5iYdjZHGgW5msmaCFWqaL77621NhPTVqd1dZEt0Bm8-huziJyUVRFxUMr-3RqgpsQcjjOQWPZOYt1ItUUfbn2O2O64QpY_q1GwLCLXcOrtwFaHq7EFMU526EdOHUGjK1-E1LxouaUcP-yE-uTS7UVdLsTUsWFvfAPJVS1zbIZbHKaQprQ-79Sa3XT4HiVFgDbUnGX0Tyw
