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