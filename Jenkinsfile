pipeline {
    agent any

    stages {
        stage("Package") {
            steps {
                sh "./gradlew build"
            }
        }

        stage("Docker build") {
            steps {
                sh "docker build -t localhost:5000/calculatrice ."
            }
        }

        stage("Docker push") {
            steps {
                sh "docker push localhost:5000/calculatrice"
            }
        }

        stage("Deploy to staging ou déployer en préproduction") {
            steps {
                sh "docker rm -f calculatrice || true"
                sh "docker run -d --rm -p 8882:8888 --name calculatrice localhost:5000/calculatrice"
            }
        }
    }
}

