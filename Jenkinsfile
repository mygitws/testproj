pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                
                sh 'rm package.zip'

                script {
                    zip zipFile:"package.zip", archive:false, glob:"**/*"
                }

                stash name: "myartifacts", includes: "**/*.zip", useDefaultExcludes:true
            }
        }
        /*
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                
                //deleteDir()
                
                sh 'ls'
                
                unstash "myartifacts"
                
                sh '''
                    ls
                    cat readme
                    cat notes
                '''
                
                sh 'chmod +x sayHello'
                sh './sayHello "Git"'
            }
        }
        */
    }
}
