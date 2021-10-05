pipeline {

    agent { dockerfile true }

    stages {
        // Building Docker images
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build 'python_server:latest'
                }
            }
        }

        // Stopping Docker containers for cleaner Docker run
        stage('Docker stop container') {
            steps {
                sh 'docker ps -f name=PythonServerContainer -q | xargs --no-run-if-empty docker container stop'
                sh 'docker container ls -a -fname=PythonServerContainer -q | xargs -r docker container rm'
            }
        }

        // Running Docker container, make sure port 8096 is opened in
        stage('Docker Run') {
            steps {
                script {
                    dockerImage.run("-p 8000:8000 --rm --name PythonServer")
                }
            }
        }
    }
}