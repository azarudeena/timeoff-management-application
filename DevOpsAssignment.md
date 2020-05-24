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

Go to Manage Jenkins -> Manage Plugins -> Select Available tab -> Search for 
[Docker](https://wiki.jenkins.io/display/JENKINS/Docker+Plugin) and install the same without Restart. 


### Configuring the Cloud 

**Pre-Requisites** : Please expose the docker host proxy in your docker as API. To test this, Please visit this [uri](http://localhost:2375/containers/json) in the host
which would provided the running containers details as json. 


*   Go to Manage Jenkins -> Manage Nodes and Clouds -> Configure Clouds -> Add a new cloud -> Select docker. 
*   Add the docker host URI as `tcp://host.docker.internal:2375` and click "**Test Connection**" to validate the Docker Verison and Docker API version. 
*   Please make sure the options Enabled check box is selected. 

### Configuring the Docker Agent Template

*   After the above step, Click on **Docker Agent Templates**, Give a Label "**nodejsapp**"(this will be import to use on deployment)
*   Provide the Docker image as "**benhall/dind-jenkins-agent:v2**" and update Remote File System root option to "**/var/run/docker.sock:/var/run/docker.sock**"
*   Select the Connect Method as "Connect with SSH" and SSH key as Inject SSH key. and user to root (* user root can be modified to user name in the host.
 Depends on how the docker options for the Jenkins master. )
*   Please make sure the options Enabled check box is selected.

Click Save. viola, We have the option for the dockerised executor can be configured with Jenkinsfile wih the above mentioned label. 


## Configuring the Time off Applications for Build. 




    




P.S. I changed the port to 9001 for Jenkins as the my host is same and would be facing the port binding issues for 8080 
for the applications as well. 
