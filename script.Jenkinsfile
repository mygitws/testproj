node {
    
    git url: 'https://github.com/mygitws/testproj.git'
    
        
    stage('Build') {
        echo 'Building...'

        sh '''
        tree
        rm -rf build tmp
        mkdir build
        mkdir tmp
        cp readme notes tmp
        '''
        
        dir ("build")
        {
            zip zipFile:"package.zip", archive:true, glob:"tmp/*"
        }
        
        stash name: "myartifacts", includes: "build/**", useDefaultExcludes:truel
    }

        
    stage('Test') {
        echo 'Testing..'
    }

    stage('Deploy') {
        echo 'Deploying....'

        sh 'ls build'
        unstash "myartifacts"
        mkdir dest
        unzip zipfFile:"build/package.zip", dir:"dest"
        sh 'ls build'
        sh 'ls dest'

        sh '''
            cat dest/readme
            cat dest/notes
        '''

        sh 'chmod +x sayHello'
        sh './sayHello "Git"'

       cleanWs notFailBuild: true
    }

    
    

}

