# Fiche aide Jenkins

<img src="https://cdn-icons-png.flaticon.com/512/9044/9044199.png" alt="brain" width="100"/>

**Continuous integration ? Continuous delivery ? Pipeline ? Script de pipeline ? Jenkins agent ?**

<img src="https://cdn-icons-png.flaticon.com/512/1336/1336682.png" alt="brain" width="100"/>

**Installer Jenkins sous Docker**
```
docker network create jenkins_network
docker run --name jenkins_container --network jenkins_network -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:lts-jdk17
```

**Installer un agent Jenkins**

// TO-DO : Ajouter une vidéo YouTube

```
docker run --name jenkins_agent_container --network jenkins_network --restart=on-failure --init jenkins/inbound-agent -url http://jenkins_container:8080 <secret> <agent name>
```
<img src="https://cdn-icons-png.flaticon.com/512/3867/3867652.png" alt="brain" width="100"/>

**Squellette de pipeline**
```
pipeline {
    agent any

    stages {
        stage("Mon nom d'étape ici") {
            steps {
                //mon code ici
            }
        }
    }
}
```

**Mon premier script de pipeline**

// TO-DO : Ajouter une vidéo YouTube

```
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```

**Etape de clone**

```
pipeline {
    agent any

    stages {
        stage('Clone the repository') {
            steps {
                git branch: 'main', url: 'https://github.com/fredericEducentre/zodiacJS.git'
            }
        }
    }
}
```
