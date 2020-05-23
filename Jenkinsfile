pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World Ale"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
                  sh 'echo "Lint work well"'
 
              }
         }
         stage('Security Scan') {
              steps { 
                 aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'Ok'
                 sh 'echo "Security Scan Work well"'
              }
         }         
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-2',credentials:'AKIAYNDFG2EULFB2JJYG') {
                  sh 'echo "Uploading content with AWS creds"'
                  s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-jenkins-pipeline')
                  }
              }
         }
     }
}
