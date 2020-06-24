pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'echo "Hello World"'
        sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                     echo "Hiiiiiiii"
                 '''
        sh 'echo hello ahmed'
      }
    }

    stage('Lint HTML') {
      steps {
        sh 'sudo tidy -q -e *.html'
      }
    }

    stage('Security Scan') {
      steps { 
        aquaMicroscanner(imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html')
      }
    }

    stage('Upload to AWS') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'S3', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        // some block
        sh 'aws s3 ls '
        sh 'echo "Create bucket" '
        sh 'aws s3 mb s3://udacityprojectthree --region us-west-2'
        sh 'aws s3 cp index.html s3://udacityprojectthree '  
        sh 'echo "Uploading content with AWS creds"'
        
      }
    }
  }
}
}
