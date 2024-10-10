<h1> Docker CheetSheet </h1>

**TODO**
1. Multicontainer application
2. Login github
3. Push / pull image
4. Execute command inside container (background mode)

<h3> Reference </h3>

1. [Docker documentation](https://docs.docker.com/reference/cli/docker/container/ls/)

<h2> Main Commands</h2> 

Show both running and stopped containers
```
docker ps -a
```

See list of images available on the host
```
docker image ls
```

Download an image
```
docker pull <image name>
```

Build and tag an image based on a docker file

```
docker build -t <accountname>/<image name> :<tag name> .
```

Run an image
```
docker run <image name>
```

Stop a container
```
docker stop <container name / contains id>
```

Get details on contaienr
```
docker inspect <container name>
```
Äccess logs of the container
```
docker logs <container name>
```


<h2> Running containers </h2>

Port mapping <port on docker host>:<port on docker container>
```
docker run -p <port on docker host>:<port on docker container> <container command>
```

Persist the data
```
docker run -v <filepath external>:<filepath docker> <package name>
```

Pass environment variables
```
docker run -e APP_COLOR=red <name>
```

Get the list of environment variables
```
docker inspect <container name> // see ENV-Vars
```

Run a docker image on a repote host
```
docker -H=10.123.2.1:<port> run <image name>
```

<h3> Running commands in the container <h3>

Execute a command in a running container
```
docker exec <container name> <command>
```

Run container in interactive mode 
```
docker run -it <container name> <command>
```

Run a docker container in the detached mode (on the background - can use command prompt)
```
docker run -d <container name>
docker attach <container id>
```

<h2> Miscellaneous </h2>

Start docker grafana
```
docker run -d -p 3000:3000 --name=grafana/grafana-oss
```

<h1> Dockerfile </h1>
**TODO**
