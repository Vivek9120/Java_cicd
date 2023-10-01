pipeline {
    agent { label 'Jenkins_Agent'}
    tools {
        jdk 'Java17'
        maven 'Maven3'

    }
    stages{
        stage("Cleanup Workspase"){
            steps{
                cleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Vivek9120/Java_cicd'
            }
            }
        
        stage("Build Application"){
            steps{
                sh "mvn clean package"
            }
        }

        stage("Test Application"){
            steps{
                sh "mvn test"
            }
        }
        stage("Sonarqube Analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token'){
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
        }
}

