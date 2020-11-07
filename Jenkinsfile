pipeline{
    agent any
    stages {
        stage('Publish') {
           environment {
               registryCredential = 'phamthanhtin0702'
           }
           steps{
               script {
                   def appimage = docker.build "node:lastest"
                   docker.withRegistry( '', registryCredential ) {
                       appimage.push()
                       appimage.push('latest')
                   }
               }
           }
       }
    }
    
    
    // agent{
    //     docker {
    //         image 'node:latest'
    //         args '-p 6001:6001'
    //     }
    // }
    // stages{
    //     stage("Setup"){
    //         steps{
    //             sh 'whoami'
    //         }
    //     }
    //     stage("Build"){
    //         steps{
    //             sh 'npm install'
    //         }
    //         post{
    //             always{
    //                 echo "========always========"
    //             }
    //             success{
    //                 echo "========A executed successfully========"
    //             }
    //             failure{
    //                 echo "========A execution failed========"
    //             }
    //         }
    //     }
    // }
    // post{
    //     always{
    //         echo "========always========"
    //     }
    //     success{
    //         echo "========pipeline executed successfully ========"
    //     }
    //     failure{
    //         echo "========pipeline execution failed========"
    //     }
    // }
}