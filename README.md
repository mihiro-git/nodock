# NoDock
Docker Compose for Node projects with MySQL and NGINX images

**WARNING: THIS PROJECT IS STILL IN EARLY DEVELOPMENT, DO NOT USE IN PRODUCTION**

## Requirements
* [Docker Engine 1.12+](https://docs.docker.com/engine/installation/)
* [Docker Compose 1.8+](https://docs.docker.com/compose/install/)

## Usage

#### Install in your project

As a submodule:
```
git submodule add https://github.com/Osedea/nodock.git
```

#### Build and Run the containers
```
cd nodock
docker-compose up -d
```

## Customization

To customize the NoDock installation, either add a `docker-compose.override.yml` in the NoDock directory or store environment specific configurations.

```
docker-compose -f nodock/docker-compose.yml -f docker-compose.dev.yml up -d
```

#### Change the node entrypoint

Use `main.js` instead of `index.js`
```
# docker-compose.override.yml

version: '2'

services:
    node:
        entrypoint: run-nodock "node main.js"
```

#### Change the MySQL environments variables
```
# docker-compose.override.yml

version: '2'

services:
    mysql:
        environment:
            MYSQL_DATABASE: custom_database
            MYSQL_USER: custom_user
            MYSQL_PASSWORD: custom_password
            MYSQL_ROOT_PASSWORD: custom_root_password
```

#### Change the NGINX reverse proxy port

Use port `8080` instead of `8000` to bind your Node server
```
# docker-compose.override.yml

version: '2'

services:
    nginx:
        build:
            args:
                reverse_proxy_port: "8080"
```

#### Change the NODE_ENV variable

The default `NODE_ENV` value is `production`, you can change it to development by doing the following
```
# docker-compose.override.yml

version: '2'

services:
    node:
        environment:
            NODE_ENV: development
```

#### Use a specific Node version

The default node version is `latest`, this is **NOT** advisable for production
```
# docker-compose.override.yml

version: '2'

services:
    node:
        build:
            args:
                node_version: 4.6.0
```
