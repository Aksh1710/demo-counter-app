pipeline{
    agent any
    stages{
        stage('Git Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Aksh1710/demo-counter-app.git' 
            }
        }
        stage('Unit Testing'){
            steps{
                sh 'mvn test' 
            }
        }
        stage('Integration testing'){
            steps{
                sh'mvn verify -DskipUnitTests'
            }
        }
        stage('Docker build'){
            steps{
                script{
                    sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID aksh3456/$JOB_NAME:v1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID aksh3456/$JOB_NAME:latest'
                }
            }
        }
        stage('push the image to docker hub'){
            steps{
                script{
                     withCredentials([string(credentialsId: 'git_creds', variable: 'Dockerhub_Cred')])
			         sh 'docker login -u aksh3456 -p $(Dockerhub_Cred)'
			        sh 'docker image push aksh3456/demoproject_1:$BUILD_ID' 
                }
            }     
        }

    }
}    


  
      
 

