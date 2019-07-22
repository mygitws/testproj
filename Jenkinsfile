pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                
                sh 'mkdir -p build/prod/release'
                script {
                    zip zipFile:"package.zip", archive:false, glob:"**/*"
                }
                sh 'cp package.zip build/prod/release'
                stash name: "myartifacts", includes: "build/prod/**/*.zip", useDefaultExcludes:true
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
                unstash "myartifacts"
                
                sh '''
                    cat build/prod/release/readme
                    cat build/prod/release/notes
                '''
                
                sh 'chmod +x sayHello'
                sh './sayHello "Git"'
            }
        }
    }
}
