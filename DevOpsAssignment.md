# DevOps Assignment 

## Configuration of Jenkins Docker

Pull the docker image of jenkins long term support image by exposing the 8080 port to 9001 port in host configure the 
jenkins master. Ideally, volumes would be mounted externally to backup the data of the Jenkins configurations in Jenkins
Home directory. Just add ``` -v <your_volume>:/var/jenkins_home``` to the below docker run command. 


```
docker run -p 9001:8080 -p 50000:50000 --name jenkins-master jenkins/jenkins:lts
```

Once the docker is the up and running, You would be provided with the default admin password to login for the first with 
the default user name as admin. The location of the password will be available in `/var/jenkins_home/secrets/initialAdminPassword`
to login. 

Once the Jenkins application is up and running. 

## Configuring the Jenkins Docker Plugins 

### Install Plugins. 

Go to Manage Jenkins -> 


P.S. I changed the port to 9001 for Jenkins as the my host is same and would be facing the port binding issues for 8080 
for the applications as well. 
