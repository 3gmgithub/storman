# Storman (MaxView for Adaptec Controllers)

Based on: [https://github.com/thomashilzendegen/docker-storman/tree/main](https://github.com/thomashilzendegen/docker-storman/tree/main)

Project GitHub: [https://github.com/3gmgithub/storman](https://github.com/3gmgithub/storman)

Project Docker Hub: [https://hub.docker.com/r/xtekllc/storman](https://hub.docker.com/r/xtekllc/storman)

StorMan data is stored in `/usr/StorMan` so we have added a vol for the data to persist in the compose.yml

compose.yml
```bash
networks:
  stor_net:
    driver: bridge
volumes:
  stor-data:

services:

  storman:
    env_file: .env
    image: xtekllc/storman:latest
    container_name: storman
    hostname: storman-docker
    privileged: true
    restart: unless-stopped
    ports:
      - 8443:8443/tcp
    networks:
      - stor_net
    volumes:
      - stor-data:/usr/StorMan
```

docker run
```bash
docker run -h storman-docker --privileged --name storman -p 8443:8443/tcp xtekllc/storman:latest
```

arcconf tool
```bash
# Command help
docker exec -it storman arcconf help

# List controllers
docker exec -it storman arcconf list
```

## ENV Var (See .env for info)
```bash

# Set the root password
STORMAN_PASS
```

## Tested with the following controllers:

```
Adaptec 6805t
Adaptec 8405
```