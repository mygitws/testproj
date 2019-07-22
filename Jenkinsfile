pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh ./sayHello
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
