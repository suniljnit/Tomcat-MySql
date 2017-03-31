Docker container: CentOS 7 + Java 8 + Tomcat 8

## Install Docker

```sh
## Remove all Packages from Yum Repo
sudo yum -y remove docker \
		docker-common \
		container-selinux \
		docker-selinux \
		docker-engine
## Setup Yum repo for latest Docker-CE Contiainer Engine

sudo yum -y install yum-utils

sudo yum-config-manager \
	--add-repo \
	https://download.docker.com/linux/centos/docker-ce.repo

sudo yum makecache fast && sudo yum -y update

sudo yum list docker-ce.x86_64 --showduplicates |sort -r

sudo yum install docker-ce-<VERSION>

sudo systemctl enable docker && sudo systemctl start docker

sudo usermod -aG docker $(whoami)

Logout and log back in 

## Confirm the Docker Version and Run a Test Container that Prints the Message and exits.

docker -v && docker run hello-world 
```

## Build the image

```sh
git clone https://github.com/ttadepalli86/tomcat.git
cd tomcat
docker build -t ttadepalli86/tomcat .
```

## How to use
Put your war under the `/opt/tomcat/webapps` directory and run the following command.

```sh
docker run -v /opt/tomcat/webapps:/opt/tomcat/webapps -v /opt/tomcat/logs:/opt/tomcat/logs -p 8080:8080 -i -t --name centos-tomcat8 ttadepalli86/tomcat
```

Once you run it, you can start the container with `docker start centos-tomcat` in next time and log file will be under the `/opt/tomcat/logs` directory.

Also, if you got some error, you can remove the container with `docker rm centos-tomcat`. Your current container list will be show with `docker ps -a`.

For Mac user, you must share the directory `/opt/tomcat/webapps` and `/opt/tomcat/logs` on Docker > Preferences > File Sharing.

## Versions
If you got error while build the docker image, please check the latest version of Java and Tomcat.

|Software|Version|Note|
|:-----------|:------------|:------------|
|CentOS|7||
|Java|8u112|[Java Release Note](http://www.oracle.com/technetwork/java/javase/8u-relnotes-2225394.html)|
|Apache Tomcat|8.5.9|[Tomcat Download Page](http://tomcat.apache.org/download-80.cgi)|

[Docker Official Image for Tomcat](https://github.com/docker-library/tomcat) is also available.
