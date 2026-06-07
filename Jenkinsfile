pipeline {
    agent { label 'spc'}
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git checkout') {
            steps {
                git url: "https://github.com/Naveenbojja01/spring-petclinic.git",
                branch: "main"
            }
        }
        stage('scan') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_ID', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('SONAR_QUBE') {
                        sh """mvn clean verify sonar:sonar \
                              -Dsonar.projectkey=Naveenbojja01_spring-petclinic \
                              -Dsonar.organization=naveenbojja01 \
                              -Dsonar.host.url=https://sonarcloud.io/ \
                              -Dsonar.login=SONAR_TOKEN"""


                    }
                }
            }
        }
    }
}