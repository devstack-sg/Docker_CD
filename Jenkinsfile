pipeline{
    agent any
    stages{
        stage("Clean"){
            steps{
                cleanWs()
            }
        }
        stage("Get Code"){
            steps{
                git branch: 'main', url: 'https://github.com/devstack-sg/Docker_CD.git'
            }
        }
        stage("Docker tag/build"){
            steps{
                sh 'docker build -t devstacksg/webapp:${image_version} .'
                
            }
        }
        stage("Docker push to registry"){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-creds') {
                        sh 'docker push devstacksg/webapp:${image_version}'
                    }
                }
            }
        }
    }
}
