**RUN WITHOUT DOCKER FILE**: `docker run --rm -it -v $(pwd)/app/:/usr/src/app -p 3000:3000 node:15 bash`
**BUILD**: `docker build -t greg0x46/hello-express .`
**BUILD Dockerfile.prod**: `docker build -t greg0x46/hello-express . -f Dockerfile.prod`
**RUN BUILDED IMAGE**: `docker run -p 3000:3000 --name hello-express greg0x46/hello-express`