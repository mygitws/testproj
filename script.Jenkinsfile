node {
    
    git url: 'https://github.com/mygitws/testproj.git'
    
    stage('Greeting') {
        echo 'Greeting..'
        
        retMsg = sh (script: './sayHello man', returnStdout: true).trim()
        echo retMsg
        
        sh 'chmod +x sayHello'
        sh './sayHello "Git"'
    }
    
    stage('Build') {
        echo 'Building...'

        sh '''
        tree
        rm -rf build tmp package.zip
        mkdir -p build/zip
        mkdir tmp
        cp readme notes tmp
        '''

        // create zip file containing tmp/notes and tmp/readme
        //  zip zipFile:"package.zip", archive:true, glob:"tmp/**"
        
        // create zip file containing notes and readme
        zip zipFile:"testpackage.zip", archive:true, glob:"*", dir:"tmp"
        sh 'unzip -l testpackage.zip'
        
        // create zip file containing notes and readme
        dir ("tmp") {
            zip zipFile:"package.zip", archive:true, glob:"notes, readme"
        }
        
        sh '''
        unzip -l tmp/package.zip
        cp tmp/package.zip build/zip
        cp tmp/readme build
        '''
        
        dir("tmp") {
            stash name: "mynotes-stash", includes: "notes"
        }
        stash name: "myartifacts-stash", includes: "build/**/*", useDefaultExcludes:true
    }

    stage('Package') {
        echo 'Packaging....'

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
        echo 'Checking artifacts and packages...'
        
        deleteDir()
        sh 'tree'
        
        unstash "mynotes-stash"
        unstash "myartifacts-stash"
        unstash "cpiopackage-stash"
        
        sh 'tree'
    }
}

