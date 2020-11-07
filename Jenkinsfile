pipeline{
    agent any
    stage('Publish') {
           environment {
               registryCredential = 'phamthanhtin0702'
           }
           steps{
               script {
                   def appimage = docker.build registry + ":$BUILD_NUMBER"
                   docker.withRegistry( '', registryCredential ) {
                       appimage.push()
                       appimage.push('latest')
                   }
               }
           }
       }
}