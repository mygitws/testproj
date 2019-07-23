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
            zip zipFile:"package.zip", archive:true, dir:"..", glob:"tmp/*"
        }
        
        stash name: "myartifacts", includes: "build/**", useDefaultExcludes:true
    }

        
    stage('Test') {
        echo 'Testing..'
    }

    stage('Deploy') {
        echo 'Deploying....'

        sh 'ls'
        unstash "myartifacts"
        mkdir dest
        //unzip zipfFile:"build/package.zip", dir:"dest"
        unzip zipfFile:"build/package.zip"
        mv build/package.zip dest
        sh 'ls build'
        sh 'ls dest'

        sh '''
            cat dest/readme
            cat dest/notes
        '''

        sh 'chmod +x sayHello'
        sh './sayHello "Git"'

        cleanWs disableDeferredWipeout: true, deleteDirs: true
    }

    
    

}

