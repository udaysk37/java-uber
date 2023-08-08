pipeline{
    
    agent any 
             environment {
           PATH="/opt/maven/bin/:$PATH"
   }    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/udaysk37/java-uber.git'
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
            stage('Docker image'){
                environment {     
                    DOCKERHUB_CREDENTIALS= credentials('DOCKER')     
                } 
                steps{
                    
                    script {
                         sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                        sh 'docker image tag $JOB_NAME:v1.$BUILD_ID udayshankar123/$JOB_NAME:v1.$BUILD_ID'
                    }
                }
            }
        }
        
}
