
### Remove all containers that are not currently running
```
docker rm `docker ps -a -q -f status=exited`
```

