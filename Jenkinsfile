pipeline{
    
    agent any 
             environment {
           PATH="/opt/maven/bin/:$PATH"
   }    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/vikash-kumar01/mrdevops_javaapplication.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Docker image'){
                
                steps{
                    
                    script{
                        sh "docker image build -t $JOB_NAME:v1.BUILD_ID"
                        sh "docker image tag $JOB_NAME:v1.BUILD_ID udayshnakr123/$JOB_NAME:v1.BUILD_ID"
                         sh "docker image tag $JOB_NAME:v1.BUILD_ID udayshnakr123/$JOB_NAME:latest"
                        
                    }
                }
            }
        }
        
}
