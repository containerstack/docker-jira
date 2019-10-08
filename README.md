# Atlassian Jira in a Docker container

This is a containerized installation of Atlassian Jira with Docker.
The aim of this image is to keep the installation easy and as straight forward as possible.

It's possible to clone this repo and build the image on you're own machine, but if you think that's a waste of time ;-) there's a Automated Build in the Docker Hub that's based on this repo.

* [Docker Hub - Automated Build](https://hub.docker.com/r/containerstack/jira/)
* [Atlassian Jira latest build](https://confluence.atlassian.com/jirasoftware/jira-software-release-notes-776821069.html)
* [Oracle MySQL Connector J latest build](http://dev.mysql.com/downloads/connector/j/)
* [Atlassian Jira](https://www.atlassian.com/software/jira)

## Versions
Currently this repo have the following versions;
* 8.3.4 (latest - not yet tested)
* 8.3.3 (latest - tested)

Go to [Branches](https://github.com/containerstack/docker-jira/branches) to see all different builds that are available.

## Use the Automated Build image for a TEST deployment;

To quickly get started running a Jira instance, use the following command:
```bash
docker run --detach \
           --name jira \
           --publish 8080:8080 \
           containerstack/jira:latest
```

Once the image has been downloaded and container is fully started (this could take a few minutes), browse to `http://[dockerhost]:8080` to finish the configuration and enter your trail/license key.

NOTE: It's not recommended to run Jira this way because it does NOT have persistent storage, once the container is removed everything is gone!!

### What does all these options do?;
detach          runs the container in the background
name            gives the container a more useful name
publish         publish a port from the container to the outside world (docker node [outside] / container [inside])


## Use the Automated Build image for a PRODUCTION deployment;

In order to make sure that what ever you or you're team is creating in Jira is persistent even when the container is recreated it's useful to make the "/var/atlassian/Jira" directory persistent.
```bash
docker run --detach \
           --name Jira \
           --volume "/persistent/storage/atlassian/Jira:/var/atlassian/Jira" \
           --env "CATALINA_OPTS= -Xms512m -Xmx4g" \
           --publish 8080:8080 \
           containerstack/Jira:latest
```

Once the image has been downloaded and container is fully started (this could take a few minutes), browse to `http://[dockerhost]:8080` to finish the configuration and enter your trail/license key.

### What does all these options do?;
| Option| Description|
| :------------- |:-------------|
|detach|*runs the container in the background*|
|name|*gives the container a more useful name*|
|volume|*maps a directory from the docker host inside the container*|
|env|*sets environment variables (this case it's for setting the JVM minimum/maximum memory 512MB<->2GB)*|
|publish|*publish a port from the container to the outside world (dockernode [outside] / container [inside])*|



## Issues, PR's and discussion

If you see an issues please create an [issue](https://github.com/containerstack/docker-jira/issues/new) or even better fix it and create an [PR](https://github.com/containerstack/docker-jira/pulls) :-)
