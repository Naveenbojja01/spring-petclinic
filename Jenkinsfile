pipeline {
    agent { label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git checkout') {
            steps {
                git url: "https://github.com/Naveenbojja01/spring-petclinic.git"
                branch: "main"
            }
        }
        stage('scan') {
            steps {
                withCredentials([string(credentialsId: 'sonar_id', variable: 'SPC_SONAR')]) {
                    withSonarQubeEnv('SONAR') {
                        sh """mvn clean verify sonar:sonar \
                              -Dsonar.projectkey=naveenbojja01 \
                              -Dsonar.organization=Naveenbojja01 \
                              -Dsonar.host.url=https://sonarcloud.io/ \
                              -Dsonar.login=SPC_SONAR"""
                    }
                }
            }
        }
    }
}