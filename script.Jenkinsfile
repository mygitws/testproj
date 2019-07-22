node {
    stage('Build') {
        echo 'Building..'

        sh '''
        rm -rf build
        mkdir build
        cp readme notes build
        dir ("build") {
            zip zipFile:"package.zip", archive:false, glob:"**/*"
        }
        '''

        stash name: "myartifacts", includes: "build/**/*.zip", useDefaultExcludes:true
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
            cat build/readme
            cat build/notes
        '''

        sh 'chmod +x sayHello'
        sh './sayHello "Git"'

        cleanWs notFailBuild: true
    }
}

