# Start docker at boot
See: [https://docs.docker.com/engine/admin/host_integration/#examples](https://docs.docker.com/engine/admin/host_integration/#examples)

Create the service file `/etc/systemd/system/docker-container@.service` for systemd:

```
[Unit]
Description=Docker Container %I
Requires=docker.service
After=docker.service

[Service]
Restart=always
ExecStart=/usr/bin/docker start -a %i
ExecStop=/usr/bin/docker stop -t 2 %i

[Install]
WantedBy=default.target
```

Enable a new container to run at boot (replace vpn with the container name):

```
systemctl enable docker-container@<container-name>.service
```

Override the default service by using the following:

```
systemctl edit docker-container@<container-name>.service
```
