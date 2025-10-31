pipeline {
    agent any
    environment {
        // Use a consistent variable name, e.g., DOCKER_IMAGE, adhering to Groovy/Shell conventions
        DOCKER_IMAGE = "hello_world_python:1.0"
    }

    stages {
        stage('Checkout') {
            steps {
                // Good practice to use sh or script block for git when using declarative pipeline
                git branch: 'main', url:'https://github.com/samcdac2025-coder/jenkins_docker_python_hello_world.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // Check for Dockerfile presence
                    if (fileExists('Dockerfile')) {
                        // Use $DOCKER_IMAGE for Groovy/environment variables in GString interpolation ("")
                        sh "docker build -t ${env.DOCKER_IMAGE} ."
                    } else {
                        // Using 'error' stops the pipeline immediately
                        error "Dockerfile not found in the workspace."
                    }
                }
            }
        }

        stage('Docker Run') {
            steps {
                // Use $DOCKER_IMAGE for Groovy/environment variables in GString interpolation ("")
                sh "docker run --rm ${env.DOCKER_IMAGE}"
            }

            post {
                success {
                    echo "Python container run completed successfully."
                }
                failure {
                    echo "There was an error running or building the container."
                }
            }
        }
    }
}

