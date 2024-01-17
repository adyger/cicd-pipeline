pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/username/cicd-pipeline.git'
        BUILD_SCRIPT_PATH = 'scripts/build.sh'
        TEST_SCRIPT_PATH = 'scripts/test.sh'
        DOCKERFILE_PATH = 'src/Dockerfile'
        DOCKER_REGISTRY_URL = 'your-docker-registry-url'
        DOCKER_IMAGE_NAME = 'epam_test_image'
    }

    stages {
        stage('Build Application') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: REPO_URL]]])
                    
                    dir('scripts') {
                        sh "chmod +x ${BUILD_SCRIPT_PATH}"
                        sh "./${BUILD_SCRIPT_PATH}"
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: REPO_URL]]])
                    
                    dir('scripts') {
                        sh "chmod +x ${TEST_SCRIPT_PATH}"
                        sh "./${TEST_SCRIPT_PATH}"
                    }
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
        
        
        
        
        
   
