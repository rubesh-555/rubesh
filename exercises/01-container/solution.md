Authenticated with Docker Hub to allow pushing and pulling images from the remote registry. 
        (docker login)

Built the Docker image from the Dockerfile in the current directory and tagged it as rubesh-hello-app.
        (docker build -t rubesh-hello-app )

Tagged the locally built image with the Docker Hub repository name to prepare it for pushing to the remote registry.
        (docker tag rubesh-hello-app rubesh28/rubesh-hello-app:latest)

Pushed the Docker image to the Docker Hub repository under the specified namespace.
        (docker push rubesh28rs/rubesh-hello-app:latest)

Started a container in detached mode, mapping host port 3000 to container port 3000, and assigned a custom container name.
        (docker run -d -p 3000:3000 --name rubesh-hello-app rubesh28rs/rubesh-hello-app:latest)

 Retrieved the runtime logs of the container to verify application startup and behavior.
        (docker logs d22747c9ab5a)

Exported the Docker image to a tar archive for backup, portability, or offline distribution. 
        (docker save -o rubesh-project.tar rubesh-hello-app:latest)
