# Installation Prerequisites for WSO2 
Note: this is my first docker image, please help me getting better. Comments are very welcome!

This image includes all prerequisites for the installation of WSO2 components and can be used as
a base image for them.

For further information on WSO2 prerequisites visit [this link](https://docs.wso2.com/display/Carbon401/Installation+Prerequisites)

Installed software in this image: Oracle Java 7, Ant, Maven, ActiveMQ

# How to use this image

Simple pull the image to use it as base for your installations.

	docker pull bastisk/wso2-preinstall

## Example: WSO2 - ESB Installation
This example uses the binaries .zip file from the official [WSO2-Website](https://wso2.com)

Download the current binary zip-file from the WSO2-Website into a folder of your choice.

Create a Dockerfile in the same directory as the downloaded file with the following content:

	FROM bastisk/wso2-preinstall
	MAINTAINER Basti SK <basti.sk@gmx.de>
	
	ENV DEBIAN_FRONTEND noninteractive
	
	# ========== 1. Install WSO2-Carbon ==========
	RUN mkdir /opt/wso2esb
	ADD wso2esb-4.8.1.zip /opt/wso2esb/wso2esb-4.8.1.zip
	WORKDIR /opt/wso2esb
	RUN unzip wso2esb-4.8.1.zip
	
	# ========== 2. Open Ports ==========
	EXPOSE 9443
	
	
	# ========== 3. Run WSO2 Server ==========
	CMD sh /opt/wso2esb/wso2esb-4.8.1/bin/wso2server.sh

Then build the image by running:

	docker build -t imagename .

If the build process is done you can run the container by executing:

	docker run -p 9443:9443 imagename

To open the Management Console of WSO2-ESB, open this address in your browser:

	https://localhost:9443/




