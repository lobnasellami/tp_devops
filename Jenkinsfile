pipeline{
    agent any
    tools {
        maven 'maven'
    }

    stages{
        stage("getting code") {
            steps {
                git url: 'https://github.com/lobnasellami/tp_devops.git', branch: 'main',
                credentialsId: 'github-credentials' //jenkins-github-creds
                sh "ls -ltr"
            }
        }

       //build de l'image
         stage("creation de image"){
            steps {                
                script {
                    echo "======== executing ========"
                        sh "mvn clean package"
            
                        sh "docker build -t devopstp ."
                       }            
                        }
                    } 
     
        stage("push to docker hub") {
            steps {                
                script {
                    echo "======== executing ========"
                        
                        sh "pwd"
                        sh "ls"
                        echo "push to hub"
                        sh "docker tag devopstp lobnasellami/devopstp:devopstp"
                        sh "docker push lobnasellami/devopstp:devopstp"
                        sh "docker run -d -p 9090:8080 lobnasellami/devopstp:devopstp"
                           }        
                        }
                    }              
                
        stage("Build container for the image ") {
            steps {                
                script {
                    echo "Running the Docker container"
                        sh "docker run -d -p 9090:8080 lobnasellami/devopstp:devopstp"
                           }        
                        }
                    }              
                }
        
            post{
                success{
                    echo "======== Setting up infra executed successfully ========"
                }
                failure{
                    echo "======== Setting up infra execution failed ========"
                }
            }
             
        }        
   /* 
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }*/
