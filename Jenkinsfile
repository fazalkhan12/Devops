pipeline
{
    agent any
    environment{
        VERSION = "${env.BUILD_ID}"
    }
stages{
    stage('Initialize'){
        def dockerHome = tool 'docker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    stage("sonar quality check"){
        agent{
            docker{
                image 'openjdk:11'
            }
        }
        steps{
            script{
                withSonarQubeEnv(credentialsId: 'sonar-token'){
                  sh 'chmod +x gradlew'
                  sh './gradlew sonarqube' 
                }
            }
        }
    }
}
}
