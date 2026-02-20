# Task 3

Had help from ChatGPT to generate the `Dockerfile` and `docker-compose.yml` files, with extensive descriptions about each part.
Had help with explaining question 5 from ChatGPT.

## Instructions

To build and run the Application throught the use of Docker, do the following.

1. Ensure Docker is installed and running on your device.
2. Open a Terminal in the folder for this file.
3. Run `docker compose up --build`.
4. In a browser, navigate to `http://127.0.0.1:5000`.
5. Refresh the page to your heart's content.

## Reflection

1. `Volumes` defines where to store the data of the database. As it points to a directory managed by docker outside the containers writeable layer, that is mounted on startup. The data is kept intact between being stopped, removed or recreated, as it is stored on the host pc.

2. The `docker-compose down` command orders docker to shut down the multicontainer. The `docker-compose down -v` command does the same, but also deletes any names volumes.

3. It needs the `depends_on: db`, to ensure it starts after the database has been started. Without this either of the services could be started first, depending on when a thread got time to run. Just because the database service is started first, does not mean it is ready to receive conenctions, which is why the `app.py` has a retry loop. As the webservice needs to connect to the database, it should be started after the database, to increase the likelyhood of it getting ready for connections within the defined attempts.

4. By running `docker-compose down -v`, clearing the volumes, followed by a `docker compose up`, with or without `--build`, you would simply be starting the multicontainer as if it has never before been run.

5. Starting the multicounter with `docker compose up`, also creates a isoloated network, which all the services are connected to, and therefore and talk to each other through. Each service's name also acts as a DNS hostname, which is then passed into `app.py` through the `DB_HOST` environmental argument.
