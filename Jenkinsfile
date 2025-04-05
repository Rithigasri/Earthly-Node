pipeline {
    agent any

    stages {
        stage('Build with Earthly') {
            steps {
                sh 'earthly +docker'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f node-earthly-container || true
                    docker run -d -p 3000:3000 --name node-earthly-container node-earthly-app:latest
                '''
            }
        }
    }
}
