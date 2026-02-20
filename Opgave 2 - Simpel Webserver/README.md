# Task 2

Had help from ChatGPT to generate the `Dockerfile`, with extensive descriptions about each part.
Also helped me with question 1. and 2. I gave it what i suspected to be the answers, and it course corrected me.

## Instructions

To build and run the Application throught the use of Docker, do the following.

1. Ensure Docker is installed and running on your device.
2. Open a Terminal in the folder for this file.
3. Run `docker build -t flask-visit-app:1.0`.
    - You can exchange the `:1.0` for anything you like to use for differentiating your versions, e.g `:latest`.
4. Optionally you can run `docker images`, to view that the image was build correctly.
5. Run `docker run --rm -p 5000:5000 flask-visit-app:1.0`
    - Exchange the `:1.0` for what ever you chose to use.
    - Omitting the `:1.0` is the same as having written `:latest`.
6. In a browser, navigate to `http://127.0.0.1:5000`.
7. Refresh the page to your heart's content.

## Reflection

1. The `-p 5000:5000` defines which port on the outside of the container is connected to which port in the container, i.e `-p HOST_PORT:CONTAINER_PORT`. In this case making a request on port 5000, translates to a request on port 5000 in the container. 

2. `host='0.0.0.0'` tells Flask to listen on all available network interfaces inside the container. This allows the application to accept connections from outside the container.

3. As long as the server runs, i.e the container, the visitor count remains. It resets when the container is restarted, as the memory in which the count is kept, is cleared.

4. To Keep the count intact between restarts, it would need to be persisted each time it is incremented, e.g via writting it to a json file or database. On startup, the current visitor count should then be loaded from the persistence storage chosen.