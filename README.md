# Pipe the Docker unix socket to a TCP port

For those times when you need to interact with your Docker daemon over a non secured TCP port, and your Docker host is configured to listen to a TLS secured TCP port (and since you can't have your Docker daemon listen to both secured AND non secured TCP ports, well, you need socat to pipe the unix socket to a non secured TCP port)


    $ docker run -v /var/run/docker.sock:/var/run/docker.sock -d --name socat  anthonydahanne/docker-socat

and then, from any containers communicating with the Docker daemon through a non secured port, just use http://socat:2375 as the Docker daemon url.

    $ docker run -d -p 8080:8080 --link socat:socat jenkins
