pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'

                script {
                    zip zipFile:"package.zip", archive:false, glob:"**/*"
                }
                
                sh 'mkdir -p build/prod/release'
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
                
                deleteDir()
                
                unstash "myartifacts"
                
                sh '''
                    ls
                    ls build/prod/release/readme
                    cat build/prod/release/readme
                    cat build/prod/release/notes
                '''
                
                sh 'chmod +x sayHello'
                sh './sayHello "Git"'
            }
        }
    }
}
