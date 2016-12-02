node {
    stage('Build') {
        try {
            deleteDir()
            checkout scm

            sh 'docker build -t php-example-app:$BUILD_NUMBER --pull=true .'
            sh 'docker tag php-example-app:$BUILD_NUMBER registry.artmann.co:5000/artmann/php-example-app:$BUILD_NUMBER'
            sh 'docker push registry.artmann.co:5000/artmann/php-example-app:$BUILD_NUMBER'

            currentBuild.result = 'Success'
        } catch(err) {
            currentBuild.result = 'Failed'
            throw err
        }
    }

    stage('Deploy') {
      try {
        sh "ssh -o StrictHostKeyChecking=no root@46.21.102.98 docker service update --image registry.artmann.co:5000/artmann/php-example-app:$BUILD_NUMBER php-example-app"
      } catch(err) {
          currentBuild.result = 'Failed'
          throw err
      }
    }
}
