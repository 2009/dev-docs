### Remove all containers that are not currently running
```
docker rm `docker ps -a -q -f status=exited`
```

### Standard docker commands
```
docker build -t friendlyname .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyname  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyname         # Same thing, but in detached mode
docker ps                                 # See a list of all running containers
docker stop <hash>                     # Gracefully stop the specified container
docker ps -a           # See a list of all containers, even the ones not running
docker kill <hash>                   # Force shutdown of the specified container
docker rm <hash>              # Remove the specified container from this machine
docker rm $(docker ps -a -q)           # Remove all containers from this machine
docker images -a                               # Show all images on this machine
docker rmi <imagename>            # Remove the specified image from this machine
docker rmi $(docker images -q)             # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
```

### Run a broken container for debugging

```
docker commit <container_id> my-broken-container &&
docker run -it my-broken-container /bin/bash
```

## Useful Links

[Docker Getting Started](https://docs.docker.com/get-started/part2/)  
[Dockerfile Reference](https://docs.docker.com/engine/reference/builder)  
[Dockerfile Best Practices](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)  
[5 ways to debug an exploding Docker container](https://medium.com/@pimterry/5-ways-to-debug-an-exploding-docker-container-4f729e2c0aa8)   
[Run multiple services in a container](https://docs.docker.com/engine/admin/multi-service_container/)
