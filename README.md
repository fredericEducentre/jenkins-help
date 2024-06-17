# Fiche aide Jenkins

<img src="https://cdn-icons-png.flaticon.com/512/9044/9044199.png" alt="brain" width="100"/>

**Continuous integration ? Continuous delivery ? Pipeline ? Script de pipeline ? Jenkins agent ?**

<img src="https://cdn-icons-png.flaticon.com/512/1336/1336682.png" alt="terminal" width="100"/>

**Installer Jenkins sous Docker**
```
docker network create jenkins_network
docker run --name jenkins_container --network jenkins_network -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:lts-jdk17
```

**Installer un agent Jenkins**

[![Install jenkins agent](https://img.youtube.com/vi/6hYeuHOOiVs/0.jpg)](https://www.youtube.com/watch?v=6hYeuHOOiVs&list=PLlnA7yc_4K0hlppiX--DNEGfi9C7dsSHb&index=4)

```
docker run --name jenkins_agent_container --network jenkins_network --restart=on-failure --init jenkins/inbound-agent -url http://jenkins_container:8080 <secret> <agent name>
```
<img src="https://cdn-icons-png.flaticon.com/512/3867/3867652.png" alt="pipeline-script" width="100"/>

**Squelette de pipeline**
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

[![Install jenkins agent](https://img.youtube.com/vi/Q5ySlzAWlbE/0.jpg)](https://www.youtube.com/watch?v=Q5ySlzAWlbE&list=PLlnA7yc_4K0hlppiX--DNEGfi9C7dsSHb&index=3
)

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

**Etape de build**

```
pipeline {
    agent {
        label 'agent-node'
    }

    stages {
        stage('Clone the repository') {
            steps {
                git branch: 'main', url: 'https://github.com/fredericEducentre/zodiacJS.git'
            }
        }
        stage('Install dependencies and build the app') {
            steps {
                sh '''
                    npm install
                    npm run build
                '''
            }
        }
    }
}
```

**Etape de test unitaire**

```
pipeline {
    agent {
        label 'agent-node'
    }

    stages {
        // Toutes les étapes précédentes
        ...
        stage('Install dependencies and build the app') {
            steps {
                sh 'npm run test'
            }
        }
    }
}
```

<img src="https://cdn-icons-png.flaticon.com/512/9044/9044199.png" alt="brain" width="100"/>

**Continuous delivery ?**

<img src="https://cdn-icons-png.flaticon.com/512/3867/3867652.png" alt="pipeline-script" width="100"/>

**Etape de construction d'image**

```
pipeline {
    agent {
        label 'agent-node'
    }

    stages {
        // Toutes les étapes précédentes
        ...
        stage('Install dependencies and build the app') {
            steps {
                sh '''
                    docker login -u <mon-utilisateur-docker-hub> -p <mon-token ou mot-de-passe>
                    docker build . -t <mon-utilisateur-docker-hub>/<mon-repository>
                    docker push <mon-utilisateur-docker-hub>/<mon-repository>
                '''
            }
        }
    }
}
```

<img src="https://cdn-icons-png.flaticon.com/512/9044/9044199.png" alt="brain" width="100"/>

**webhook ?**

<img src="https://cdn-icons-png.flaticon.com/512/7098/7098010.png" alt="mouse" width="100"/>

// TO-DO : Ajouter une vidéo YouTube

<img src="https://cdn-icons-png.flaticon.com/512/9044/9044199.png" alt="brain" width="100"/>

**Serveur SMTP ?**

// TO-DO : Ajouter une vidéo YouTube
