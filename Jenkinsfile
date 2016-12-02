node {
    stage('Build') {
        try {
            deleteDir()
            checkout scm

            wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'XTerm']) {
                sh 'docker build -t php-example-app:$BUILD_NUMBER --pull=true .'
                sh 'docker tag php-example-app:$BUILD_NUMBER registry.artmann.co:5000/artmann/php-example-app:$BUILD_NUMBER'
                sh 'docker push registry.artmann.co:5000/artmann/php-example-app:$BUILD_NUMBER'
            }
            currentBuild.result = 'Success'
        } catch(err) {
            currentBuild.result = 'Failed'
            throw err
        }
    }

    stage('Deploy') {

    }
}
