rasdaman_docker
===============
This repository is our version of `https://github.com/mappl/rasdaman_docker`.
It contains all sources to build a docker image hosting a rasdaman server. 
The image includes the necessary postgres database. 
Furthermore additional tooling was added to provide a reasonable shell within the image.
For our purposes also an R studio server was added.

This image main use-case is aiding the development of raster data applications.
It is not fit for use in production.

The image exposes the following ports:
* SSH: Port 22
* Petascope: http://localhost:8080/rasdaman/ows
* RStudio: http://localhost:8787/

Example for running a container:

``docker run -d --restart=always --name=rasdaman -p 9000:8080 -p 9001:8787 -p 9002:22 -v /local/data/directory/:/opt/shared docker.disy.net/rasdaman:latest``


/Original README.md:/

A Docker image for running Rasdaman including petascope and rasgeo extensions.

# News
- (2015-02-13) RStudio Server added for client access to RRasdaman 
- (2015-02-13) RRasdaman package building added
- (2015-02-13) Rasgeo commands are currently not working due to file system blob storage 
- (2015-02-13) Now works with file system blob storage

# Prerequisites
- [Docker](https://www.docker.com/)
- At least 16 gigabytes free disk space

# Instructions
1. If not yet done, install Docker, e.g. by `sudo apt-get update && sudo apt-get install docker.io` or similar depending on your OS.
2. Download the source e.g. by `git clone https://github.com/mappl/rasdaman_docker` 
3. Make relevant scripts executable `chmod +x install.sh start.sh stop.sh`.
4. If you do not want to use the default settings for docker image and container names, hostnames, and port mapping, you may want to edit the docker run command in install.sh
5. Run `sudo ./install.sh`.
6. The image will be built and a corresponding container will be created automatically. The container will be started automatically but might still need some seconds for first time initializations (e.g. web application deployment). You can now start and stop the container whenever you like via `sudo ./start.sh` and `sudo ./stop.sh` respectively.
7. Once started, you can log in to the container via ssh using `ssh -p 21210 rasdaman@localhost`. Default password is "rasdaman".
8. From the host machine, try to access the Petascope interface or RStudio using the URL `http://localhost:21211/rasdaman/ows` and `http://localhost:21215/` respectively.



# Limitations
This is a preliminary version, open issues include the following:
- Rasgeo extension currently not working as it cannot connect to file system storage
- Rasdaman server configuration is not yet editable as install.sh arguments
- Docker run parameters like port mappings, hostnames, and mounted volumes are not yet editable as install.sh arguments
- Data directory of BLOBS is currently not accessible for the host system


