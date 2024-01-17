pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/adyger/cicd-pipeline.git'
        BUILD_SCRIPT_PATH = 'scripts/build.sh'
        TEST_SCRIPT_PATH = 'scripts/test.sh'
        DOCKERFILE_PATH = 'src/Dockerfile'
        DOCKER_REGISTRY_URL = 'https://hub.docker.com/u/adyger'
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
                try {
                    sh "docker info"
                    sh "docker build -t adyger/adr_docker_image ."
                } catch (Exception e) {
                    echo "Failed to build Docker image: ${e}"
                    error("Docker build failed.")
                }
            }
        }
    }  
}  
}
        
        
        
        
        
        
        
        
        
   
