##General 

####Basic commands
- `docker`: show a list of commands and their descriptions.
- `docker ps`: list active containers.
- `docker ps -a`: list all containers.
- `docker start <container>`: start a container
- `docker stop <container>`: stop a container
- `docker rm <container>`: remove a container.
- `docker rm <container> -f`: remove a container with force option.
- `docker ps -a -q`: list id of all containers.
- `docker build <container-registry-user>/<image>:<version> <docker-file-path>`: build an imagem by docker file.
- `docker login`: login dockerhub.
- `docker logout`: logout dockerhub.

####Docker run
- `docker run <image>`: run a container from a image in the latest tag.
- `docker run <image>:<tag>`: run a container from a image in the specific tag.
- `docker run -i <...>`: -i means interactive, attach terminal to container.
- `docker run -t <...>`: -t means tty, allows to run commands in the terminal.
- `docker run -it <...> bash`: run a container with -i and -t options and open a bash in the terminal.
- `docker run --rm <...>`: remove the conteiner after your execution.
- `docker run -p <host-port>:<container-port> <...>`: link a port from docker host to a port from docker container.
- `docker run -d <...>`: -d option means detached, detached the terminal (background).
- `docker run --name <name>`: set a name for container.
- `docker run -v <docker-host-path>:<docker-container-path> <...>`: mapping a folder from docker host to docker container, create folder if not exists.
- `docker run --mount type=bind,source=<docker-host-path>,target=<docker-container-path>`: best way to mapping a folder from docker host to docker container.
- `docker run --mount type=volume,source=<volume-name>,target=<docker-container-path>`: mapping a volume to docker container.

##Volume

####Basic commands
- `docker volume`: show a list of commands and their descriptions.
- `docker volume ls`: show a list of volumes.
- `docker volume create <name>`: create a volume.
- `docker volume inspect <name>`: show details of the volume.
- `docker volume prune`: Remove all unused local volumes

##Images

####Basic commands
- `docker pull`: download an image
- `docker push <container-registry-user>/<image>:<version>`: send a image to docker hub.
- `docker rmi <image>:<tag>`: remove an image


##Dockerfile

####File sintaxe
- `FROM <image>:<version>`: define image from container registry.
- `ENV <var> <value>`: set a env variable
- `USER <user>`: define a user (default is root), this user needs to exist.
- `WORKDIR <container-path>`: "path root" of the cointaner.
- `RUN <command>`: run a command
- `COPY <docker-host-path> <docker-container-path>`: copy a file from host do container, "\<docker-host-path\>" is relative to path of Dockerfile.
- `EXPOSE <port>`: Expose a port of container.
- `ENTRYPOINT ["echo", "Hello World"]`: "ENTRYPOINT" run in the end like "CMD", but him will always run and cannot be overwritten in the run command.
- `CMD ["echo", "Hello World"]`: "CMD" runs in the end, it can be overwritten by command, example `docker run <...> bash`, the "bash" command wil overwrite `["echo", "Hello World"]`


##Network 

####Types of network
- **bridge** (default): communication between containers.
- **host**: merge docker host network and containers network.
- **overlay**: merge network between diferent containers.
- **maclan**:  assign a MAC adress to each containers, making it appear to be a physical network interface.
- **none**: without network.

####Commands of network    
- `docker network`: show a list of docker network commands and their descriptions.
- `docker network create --driver bridge mynetwork`: example of create network command.
- `docker run <...> --network mynetwork`: example of command to run a container with custom network.
- `docker network connect <network> <container>`: connect a container in a network.


##Hacks
- `docker rm $(docker ps -a -q) -f` : remove all containers.
- `curl http://host.docker.internal:8000`: 
"http://host.docker.internal" is the docker host address, which can be accessed from a container, in this example it does an CURL on localhost of docker host on port 8000.
- `docker run --mount type=bind,source="$(pwd)"/html,target=<docker-container-path>`: "$(pwd)" can be use to be represents current folder.
- `RUN apt-get update && apt-get install -y`: In Dockerfile context "&&" can be use to run more than command sequentially and "-y" to confirm installation without interaction.
-`\`: In Dockerfile context "\\" can be used to execute commands on different lines as if they were on the same line. 
`````
RUN apt-get update && \ 
    apt-get install -y
`````
