# Final Project Casting Agency

## Casting Agency

The Casting Agency models a company that is responsible for creating movies and managing and assigning actors to those movies. You are an Executive Producer within the company and are creating a system to simplify and streamline your process.

1. Get Actors
2. Save Actors to Database
3. Update Actors
4. Delete Actors
5. Get Movies
6. Insert Movie to Database
7. Update Movie
8. Delete Movie

Base URL: `https://casting-agency-udacity.herokuapp.com/`

## About the Stack

- **SQLAlchemy ORM** to be our ORM library of choice
- **PostgreSQL** as our database of choice
- **Python3** and **Flask** as our server language and server framework
- **Flask-Migrate** for creating and running schema migrations

## Getting Started

### Installing Dependencies

1. Initialize and Setup virtual environment

```bash
py -m venv venv
```

2. Active the virtual environment

```bash
source venv/bin/activate
```

3. Install the dependencies:

```bash
$ pip install -r requirements.txt
```

## Database Setup

Adjust the database settings in the config.py file with the postgres installed on your local computer

```bash
db_setting = {
   "db_name" : "casting_agency",
   "username" : "postgres",
   "password" : "postgres",
   "port" : "localhost:5432"
}
```

Running migrations using our manage.py file.

```bash
python manage.py db init
python manage.py db migrate
python manage.py db upgrade
```

## Running the Server Locally

To run the server, execute:

```bash
python app.py
```

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
   - in API Settings:
     - Enable RBAC
     - Enable Add Permissions in the Access Token
5. Create new API permissions:
   - `get:actors`
   - `post:actors`
   - `patch:actors`
   - `delete:actors`
   - `get:movies`
   - `post:movies`
   - `patch:movies`
   - `delete:movies`
6. Create new roles for:
   - Casting Assistant
     - can `get:actors`
     - can `get:movies`
   - Casting Director
     - can `delete:actors`
     - can `get:actors`
     - can `get:movies`
     - can `patch:actors`
     - can `patch:movies`
     - can `post:actors`
   - Executive Producer
     - can `delete:actors`
     - can `delete:movies`
     - can `get:actors`
     - can `get:movies`
     - can `patch:actors`
     - can `patch:movies`
     - can `post:actors`
     - can `post:movies`
     - can perform all actions

## Testing

To run the tests, run

```bash
python test_app.py
```

## API Reference

### Getting Started

- Base URL: The backend is hosted at `https://casting-agency-udacity.herokuapp.com/`
- Authentication: This version require authentication or API keys.

### Error Handling

Errors are returned as JSON in the following format:<br>

    {
        "success": False,
        "error": 404,
        "message": "resource not found"
    }

### Endpoints

#### GET /actors

- General: Returns a list actors.
- Sample: `curl --request GET 'https://casting-agency-udacity.herokuapp.com/actors' -H "Authorization: Bearer ${TOKEN}"`<br>

            {
                "actors": [
                    {
                        "age": 32,
                        "gender": "Male",
                        "id": 1,
                        "name": "Jack Torrance"
                    }
                ],
                "success": true
            }

#### POST /actors

- General: Creates a actor using JSON Body.
- Sample: `curl -d '{"name": "Rose", "age": "20", "gender": "Female"}' -X POST https://casting-agency-udacity.herokuapp.com/actors -H "Authorization: Bearer ${TOKEN}" -H "Content-Type: application/json"`<br>

            {
                "created": 3,
                "success": true
            }

#### PATCH /actors/<actor_id>

- General: Update actor.
- Sample: `curl -d '{"age": "45"}' -X PATCH https://casting-agency-udacity.herokuapp.com/actors/1 -H "Authorization: Bearer ${TOKEN}" -H "Content-Type: application/json"`<br>

          {
              "actor": [
                  {
                      "age": 45,
                      "gender": "Male",
                      "id": 1,
                      "name": "Jack Torrance"
                  }
              ],
              "success": true,
              "updated": 1
          }

#### DELETE /actors/<actor_id>

- General: Delete actor.
- Sample: `curl -X DELETE https://casting-agency-udacity.herokuapp.com/actors/1 -H "Authorization: Bearer ${TOKEN}"`<br>

          {
            "deleted":"1",
            "success":true
          }

#### GET /movies

- General: Returns a list movies.
- Sample: `curl --request GET 'https://casting-agency-udacity.herokuapp.com/movies' -H "Authorization: Bearer ${TOKEN}"`<br>

          {
            "movies":[
                {
                  "id":1,
                  "release_date":"Fri, 10 Apr 2020 00:00:00 GMT",
                  "title":"The Shinning"
                },
                {
                  "id":2,
                  "release_date":"Fri, 10 Apr 2020 00:00:00 GMT",
                  "title":"Pycsho"
                }
            ],
            "success":true
          }

#### POST /movies

- General: Creates a movie using JSON Body.
- Sample: `curl -d '{"title": "Hysteria", "release_date": "2020-04-10"}' -X POST https://casting-agency-udacity.herokuapp.com/movies -H "Authorization: Bearer ${TOKEN}" -H "Content-Type: application/json"`<br>

            {
              "created": 3,
              "success": true
            }

#### PATCH /movies/<movie_id>

- General: Update movie.
- Sample: `curl -d '{"title": "The Shining Extended"}' -X PATCH https://casting-agency-udacity.herokuapp.com/movies/1 -H "Authorization: Bearer ${TOKEN}" -H "Content-Type: application/json"`<br>

            {
               "edited":1,
               "movie":[
                  {
                     "id":1,
                     "release_date":"Fri, 10 Apr 2020 00:00:00 GMT",
                     "title":"The Shining Extended"
                  }
               ],
               "success":true
            }

#### DELETE /movies/<movie_id>

- General: Delete actor.
- Sample: `curl -X DELETE https://casting-agency-udacity.herokuapp.com/movies/1 -H "Authorization: Bearer ${TOKEN}"`<br>

          {
            "deleted":"1",
            "success":true
          }
