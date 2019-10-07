# Sample CI / Ansible Setup

## VagrantFile and provisioning

Vagrant file spins up two servers `ci` and `app`. On the `ci` server, we install ansible (with yum)

Need to generate a private key on `ci`. 
```
ssh-keygen -t rsa -b 4096 -C "odm-ci"

```
ssh into ci
```
vagrant ssh ci
```
ssh into app
```
vagrant ssh app
```

## To start jenkins

```bash
docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock -v /usr/local/bin/docker:/usr/local/bin/docker jenkins/jenkins:lts
```

There is a docker-compose file, but I usually use the command, and it remembers my settings, somehow the docker-compose file would make me set up a new jenkins instance.

## Keys and such

Two keys are generated  `jenkins_key` and `jenkins_slave_key`. 

### jenkins_key

private key is set up as a credential in jenkins.
public key is added to `authorized_keys` in `ci` server

### jenkins_slave_key

private key is added to `ci` server under `/home/jenkins/.ssh/jenkins_key`
public key is added to `authorized_keys` in `app` server


