pipeline {
    agent any

    stages {
        stage('Docker Push') {
            steps {
                script {
                    def tag = "build-${env.BUILD_NUMBER}"
                    withCredentials([usernamePassword(credentialsId: 'Dockerhub-mosazhaw', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://host.docker.internal:2375
                            docker login -u $USERNAME -p $PASSWORD
                            docker push heussflo/node-web-app:latest
                        '''
                    }
                }
            }
        }
        stage('Trigger Render Deployment') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'RenderDeployKey', variable: 'KEY')]) {
                        sh "curl $KEY"
                    }
                }
            }
        } 
    }
}
