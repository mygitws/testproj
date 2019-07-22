node {
    stage('Build') {
        echo 'Building..'

        //sh 'rm package.zip'
        deleteDir()
        
        zip zipFile:"package.zip", archive:false, glob:"**/*"

        stash name: "myartifacts", includes: "**/*.zip", useDefaultExcludes:true
    }
        
    stage('Test') {
        echo 'Testing..'
    }

    stage('Deploy') {
        echo 'Deploying....'

        sh 'ls'

        unstash "myartifacts"

        sh '''
            ls
            cat readme
            cat notes
        '''

        sh 'chmod +x sayHello'
        sh './sayHello "Git"'

        cleanWs notFailBuild: true
    }
}

