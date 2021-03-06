# Dockerfile for osrm-backend
This container run [osrm-backend](https://github.com/Project-OSRM/osrm-backend) project.
Open Source Routing Machine (OSRM) Docker Image [\[Docker Hub\]](https://hub.docker.com/r/cartography/osrm-backend-docker/)

## Installation

1. Install [Docker](https://www.docker.com/)

2. Manual deploy (optional).

  Pull automated build from Docker Hub:
  ```
  $ docker pull cartography/osrm-backend-docker
  ```
  or build from GitHub:
  ```
  $ docker build -t="cartography/osrm-backend-docker" github.com/cartography/osrm-backend-docker
  ```
  or you can clone & build:  
  ```
  $ git clone http://github.com/greatea/osrm-backend-docker.git  
  $ docker build -t="leon/osrm-backend-docker" osrm-backend-docker/
  ```

## Usage
Run it:  
```
docker run -d -p 5000:5000 cartography/osrm-backend-docker:latest osrm label "http://your/path/to/data.osm.pbf"
```  

Explanation:  
- `-d` - run container in background and print container ID 
- `-p 5000:5000` - publish a container port to host
- `osrm` - go via entrypoint script, w/o osrm keyword - classic mode
- `label` - your label of OSM data
- `url` - link to OSM data in PBF format

For example:  
```
docker run -d -p 5000:5000 --name osrm-api cartography/osrm-backend-docker:latest osrm California "http://download.geofabrik.de/north-america/us/california-latest.osm.pbf"
```

## Start OSRM Frontend

    docker run -d --link osrm-api:api --name osrm-mos-front --restart=always -p 8080:80 cartography/osrm-frontend-docker

You must `--link` osrm-frontend container with osrm-api with `api` tag. Or use `API_PORT_5000_TCP_ADDR` and `API_PORT_5000_TCP_PORT` variables to set host and port of the api.

You can test it by visiting [http://container-ip:8080](http://container-ip:8080)
