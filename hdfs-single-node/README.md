# Single Node Hadoop File System Setup

Assuming that docker is already setup and running, execute the following commands.

### Building Image
In the folder with `Dockerfile` execute the following command:
```
docker build -t hadoop-single-node .
```
This will build the required image and put it in your local

### Running Container
Execute the following command to run the image container:
```
docker run -p 50070:50070 --rm -it hadoop-single-node:latest /bin/bash
```

`-p` : Exposes the namenode UI port

`--rm` : Removes the container after it exits. This parameter can be removed

`hadoop-single-node:latest` : Name of the image
