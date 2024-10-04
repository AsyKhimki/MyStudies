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


<h2> Miscellaneous </h2>

Start docker grafana
```
docker run -d -p 3000:3000 --name=grafana/grafana-oss
```
