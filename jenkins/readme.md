```
docker run -d jenkins/jenkins

docker run -p 8080:8080 -p 50000:50000 -d jenkins/jenkins:lts
docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts-jdk17


#my solution
https://medium.com/@yassine.essadraoui_78000/jenkins-docker-in-docker-b7630c7b9364


docker build -t jenkinscontroller ./jenkins_controller
docker run -dit --restart=always -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home --privileged -v /var/run/docker.sock:/var/run/docker.sock jenkinscontroller

docker build -t jenkinsagent ./jenkins_agent

launc agent with container command
docker run -i --rm --name agent --privileged -v /var/run/docker.sock:/var/run/docker.sock --init jenkinsagent java -jar /usr/share/jenkins/agent.jar


docker build -t jenkins-agent ./jenkins_agent


controller:
docker build -t jenkinscontroller ./jenkins_controller
docker run -d --name my-container --hostname my-hostname my-image
docker run -dit \
    --restart=always \
    -p 8080:8080 -p 50000:50000 \
    -v jenkins_home:/var/jenkins_home \
    --hostname jenkinscontroller --name jenkinscontroller jenkinscontroller


Agent:
docker build -t jenkins-agent ./jenkins_agent

docker run -d \
    --name jenkins-agent \
    -e SSH_USERNAME=jenkins \
    -e SSH_PASSWORD=password \
    -e SSH_HOST=<JENKINS_CONTROLLER_IP> \
    -e SSH_PORT=22 \
    jenkins-agent

Replace <JENKINS_CONTROLLER_IP> with the IP address or hostname of your Jenkins controller. (agent shell be the same network)

docker run -d \
    --name jenkins-agent \
    --hostname jenkinsagent \
    -e SSH_USERNAME=jenkins \
    -e SSH_PASSWORD=password \
    -e SSH_HOST=jenkinscontroller \
    -e SSH_PORT=22 \
    jenkins-agent



docker compose -f dockercompose.yaml up -d
docker compose -f dockercompose.yaml down





Configure Jenkins:
In the Jenkins web interface, navigate to Manage Jenkins -> Manage Nodes and Clouds -> Configure Clouds. Add a new cloud of type SSH Build Agents and configure it to connect to the Docker container. Provide the SSH credentials (jenkins/password in this case) and the remote root directory where Jenkins should run jobs.


Launch method: Choose "Launch agents via SSH" from the dropdown.

Host: Enter the hostname or IP address of the Jenkins agent container (e.g., jenkins-agent).

Credentials: Click on "Add" to add SSH credentials for connecting to the Jenkins agent container. Choose the following options:

Kind: Username with password
Scope: Global
Username: Enter the SSH username (e.g., jenkins).
Password: Enter the SSH password (e.g., rootroot).
ID: Provide an ID for the credentials.
Description: Optionally, provide a description for the credentials.


Create a Jenkins job:
Create a new Jenkins job and configure it to run on the newly created SSH build agent. When configuring the job, specify the label of the agent configured in the cloud settings.

Run the Jenkins job:
Start the Jenkins job and verify that it runs on the Docker container (Jenkins agent) via SSH.


Launch method
Launch agents via SSH

Host
jenkins-agent

The Host must be specified
Credentials
?

- none -
The selected credentials cannot be found
Host Key Verification Strategy
?

Known hosts file Verification Strategy
?
Advanced

```