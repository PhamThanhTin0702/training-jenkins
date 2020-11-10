pipeline{
    agent any
    stages {
    //     stage('Publish') {
    //        environment {
    //            registryCredential = 'phamthanhtin0702'
    //        }
    //        steps{
    //            script {
    //                def appimage = docker.build "phamthanhtin0702/node:lastest"
    //                docker.withRegistry( '', registryCredential ) {
    //                    appimage.push('latest')
    //                }
    //            }
    //        }
    //    }

       stage('Installation') {
           steps{
                sh "whoami"
                sh "sudo apt-get update && apt-get install -y apt-transport-https && ca-certificates curl gnupg2 && software-properties-common"
                sh "sudo curl -fsSL https://download.docker.com/linux/debian/gpg && apt-key add -"
                sh "sudo apt-key fingerprint 0EBFCD88"
                sh """
                    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian ${lsb_release -cs} stable"
                """
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