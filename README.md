This project is an example of a dockerized app using a MEAN stack (mongodb node express and Angular).

It presents 4 containers:
  - proxy: reverse proxy using nginx.
  - frontend: basic Angular app (created with angular-cli)
  - backend: basic node app (using Express)
  - database: container that includes a database (Mongo DB)

RUN

    1. Install docker and docker-compose
    2. Execute "docker-compose up"
    3. Open your browser and type "http://localhost:8080"


NOTES
    - Proxy:
        * it serves just as a reverse proxy to access the front and back ends
    - Front end
        * it can be accessed via proxy (localhost:8080) or directly (localhost:4200)
        * it has been created with angular-cli (ng new project_name). the only modification comes in the following files:
            - src/app/app.component.html
                the actual page
            - .angular-cli.json
                in order to be able to access it in a docker container we needed to add this snippet:
                "serve": {
                    "port": 4200,
                    "host": "0.0.0.0"
                }
    - Back end
        * the backend app can be accessed via the proxy (localhost:8081) or directly (localhost:3000)
    - Database
        * it is listening on port 27017
        * the backend is not really using it. Nothing is being saved and it serves just as an example of how it can be dockerized
