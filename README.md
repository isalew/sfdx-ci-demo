# SFDX CI Demo

Demonstrating the use of [Salesforce DX](https://developer.salesforce.com/platform/dx) with a Jenkins CI server.

## CI Server Setup

Download the repo

```bash
$ git clone https://github.com/isalew/sfdx-ci-demo
$ cd sfdx-ci-demo
```

Build a docker image from the project `Dockerfile`

```bash
$ docker build -t isalew/sfdx-ci .
```

Execute a container from the docker image mapped to a local volume

```bash
$ docker run -d -p 8080:8080 -v ~/repos/sfdc/sfdx/repos/sfdx-ci-demo:/sfdx-ci-demo --name sfdx-ci isalew/sfdx-ci
```

Grab the initial admin password for Jenkins from the install logs

```bash
$ docker logs -f ci
# Copy the initial password from the log file
# Open jenkins at `http://localhost:8080`, enter the initial password, and setup your admin user
```

Setup ssh for easier git repository access

```bash
$ docker exec -it ci bash
$ root@########:/# cd ~/.ssh/
$ ssh-keygen -t rsa -C 'admin@sfdx-cli'
$ cat id_rsa.pub
# Copy the public key to your github repo
```

## Additional Resources

- [How to Setup Git Repository and Credentials for Jenkins Jobs](http://www.thegeekstuff.com/2016/10/jenkins-git-setup/)
- [DockerDX: Docker Image for Salesforce DX](https://hub.docker.com/r/dancinllama/dockerdx/)
