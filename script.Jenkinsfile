node {
    
    git url: 'https://github.com/mygitws/testproj.git'
    
    stage('Greeting') {
        echo 'Greeting..'
        sh 'chmod +x sayHello'
        sh './sayHello "Git"'
    }
    
    stage('Build') {
        echo 'Building...'

        sh '''
        tree
        rm -rf build tmp
        mkdir build/zip
        mkdir tmp
        cp readme notes tmp
        '''

        zip zipFile:"package.zip", archive:true, dir:"..", glob:"tmp/*"
        sh 'mv package.zip build/zip'
        sh 'mv tmp/readme build'

        stash name: "myartifacts-stash", includes: "build/**/*", useDefaultExcludes:true
    }

    stage('Deploy') {
        echo 'Deploying....'

        sh 'ls'
        deleteDir()
        unstash "myartifacts-stash"
        
        sh '''
        tree
        cp build/zip/package.zip .
        cp build/readme .
        
        FILES="readme package.zip"
        for i in $FILES; do
            echo $i; done | cpio -ov -H crc >  cpiopackage.pkg
        #check content of cpiopackage.pkg
        cpio -itv < cpiopackage.pkg
        
        mkdir build/pkg
        mv cpiopackage.pkg build/pkg
        '''

        stash name: "cpiopackage-stash", includes: "build/pkg/*.pkg", useDefaultExcludes:true
    }
    
    stage('Check artifacts') {
        echo 'Checking artifacts...'
        
        deleteDir()
        sh 'tree'
        
        unstash "myartifacts-stash"
        unstash "cpiopackage-stash"
        
        sh 'tree'
    }
}

