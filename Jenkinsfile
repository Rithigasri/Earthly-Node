pipeline {
    agent any

    stages {
        stage('Build with Earthly') {
            steps {
                sh '''
                    if ! command -v earthly &> /dev/null; then
                        curl -LO https://github.com/earthly/earthly/releases/latest/download/earthly-linux-amd64
                        chmod +x earthly-linux-amd64
                        sudo mv earthly-linux-amd64 /usr/local/bin/earthly
                    fi

                    earthly +docker
                '''
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
