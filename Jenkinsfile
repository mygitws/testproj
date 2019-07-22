pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh ./sayHello "Git"
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
