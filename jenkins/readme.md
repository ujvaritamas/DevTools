```
docker run -d jenkins/jenkins

docker run -p 8080:8080 -p 50000:50000 -d jenkins/jenkins:lts

docker run -d -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts-jdk17
```