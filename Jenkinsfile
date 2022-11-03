pipeline {
    agent any
        stages {
          stage('Build') {
            steps {
                // Get some code from a GitHub repository
                 git branch: 'main',
                    url: 'https://github.com/zeyad133/LastProject-part2.git'

            }
        }
        stage('CI') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'dockerhubkey', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')])
                {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    sh "docker build -t appimage22 ."
                    sh "docker tag appimage22:latest zeyad13/appimage22"
                    sh "docker push zeyad13/appimage22"
                    
                }
            }    
        }
         stage ('dep app'){
            steps {
            
                          sh """
                    kubectl apply -f app-deployment.yml -n application
                    kubectl apply -f app-svc.yml -n application

                echo done
            """
            }
        
        }
    }
}
