# Nginx Mastery

## Getting Started with Nginx | Docker | Docker Compose
Nginx is an open source software for
- web serving
- proxying
- caching
- load balancing
- media streaming
- ...

In a typical web browser request-response cycle, Nginx serve as a middleman (in a basic scenario) were all requests go through it and response from the server passes it (making it birectional). At that point in the cycle, there's a lot of functionalities that can be considered before deploying the application at scale.


### Pull nginx image from [DockerHub](https://hub.docker.com)
```bash
docker pull nginx
```

### Running nginx in docker
```
docker run -it --rm -d -p 8000:80 --name website nginx
```
- `-it`: Runs the container in interactive(bash) mode
- `--rm`: 
- `-d`: Runs the container in daemon mode. That means our container can listen in the background
- `-p`: Specifies the port to listen from and to forward to. The order is in `to`:`from`. So `8000`:`80` listens from 80 from forwards to port `8000` on our local machine
- `--name`: Not required, this specifies the name to assign to the container created

### Verifying your nginx installation
```bash
curl localhost:8000
```
You can also load `localhost:8000` in your web browser

### Spawn a bash shell
```bash
docker exec -it website bash
```

### Check nginx version (In Nginx Container bash)
```bash
nginx -v
```

### Check the running processes in the nginx container
```bash
docker top website
```

### Nginx service management (In Nginx Container bash)
To start nginx: `service nginx start`

To stop nginx: `service nginx stop`

Note that stopping the nginx service shuts down the container