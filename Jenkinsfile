pipeline{

    agent any 

    environment{
        DOCKERHUB_USERNAME = "aakarsh911"
        APP_NAME = "dev-ops"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}/${APP_NAME}"
        REGISTRY_CREDS = "dockerhub"
    }

    stages{
        stage('Cleanup workspace'){
            steps{
                script{
                    cleanWs()
                }
            }

        }
        stage('Checkout DCM'){
            steps{
                script{
                    git credentialsId: 'github',
                    url: 'https://github.com/Aakarsh911/dev-ops.git',
                    branch: 'main'
                }
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage('Push Docker Image'){
            steps{
                script{
                    docker.withRegistry('', REGISTRY_CREDS){
                        docker_image.push("$BUILD_NUMBER")
                        docker_image.push("latest")
                    }
                }
            }
        }
    }
}
//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