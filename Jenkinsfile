pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/adyger/cicd-pipeline.git'
        BUILD_SCRIPT_PATH = 'scripts/build.sh'
        TEST_SCRIPT_PATH = 'scripts/test.sh'
        DOCKERFILE_PATH = 'src/Dockerfile'
        DOCKER_REGISTRY_URL = 'https://hub.docker.com'
        DOCKER_IMAGE_NAME = 'adr_docker_image:v1'
        DOCKER_REGISTRY_USER = 'adyger'
        DOCKER_REGISTRY_PASSWORD = 'dckr_pat_1qvlNzIEIu7m2UkWokWKOtD7a6A'
    }

    stages {
        stage('Build Application') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: REPO_URL]]])
                    
                    // Add commands to make the build script executable and then run it
                    sh "chmod +x ${BUILD_SCRIPT_PATH}"
                    sh "./${BUILD_SCRIPT_PATH}"
                }
            }
        }
    stage('Run Tests') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: REPO_URL]]])
                    
                    // Add commands to make the test script executable and then run it
                    sh "chmod +x ${TEST_SCRIPT_PATH}"
                    sh "./${TEST_SCRIPT_PATH}"
                }
            }
        }
        

        stage('Build Docker Image') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: REPO_URL]]])
                    
                    dir('src') {
                        // Assuming Docker is installed on the Jenkins agent
                        sh "docker build -t adyger/${DOCKER_IMAGE_NAME} ."
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_REGISTRY_USER', passwordVariable: 'DOCKER_REGISTRY_PASSWORD')]) {
                    sh """
                        docker login -u ${DOCKER_REGISTRY_USER} -p ${DOCKER_REGISTRY_PASSWORD}
                        docker push adyger/${DOCKER_IMAGE_NAME}
                        docker logout
                    """
                }
            }
        }
    }
}
        
   
        
        
        
        
        
   
