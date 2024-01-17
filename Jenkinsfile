pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/adyger/cicd-pipeline.git'
        BUILD_SCRIPT_PATH = 'scripts/build.sh'
        TEST_SCRIPT_PATH = 'scripts/test.sh'
        DOCKERFILE_PATH = 'https://github.com/adyger/cicd-pipeline.git'
        DOCKER_REGISTRY_URL = 'https://hub.docker.com/repository/docker/adyger'
        DOCKER_IMAGE_NAME = 'adr_docker_image'
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
    }
}
        
        
// ${DOCKER_REGISTRY_URL}        
        
        
        
        
        
   
