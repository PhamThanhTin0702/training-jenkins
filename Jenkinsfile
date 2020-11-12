pipeline{
    agent {label "window-slave"}
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
                git url: 'https://github.com/PhamThanhTin0702/training-jenkins.git', branch: 'main'
           }
       }

       stage('Deploye') {
           steps {
               script {
                   kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "mykuceconfig")
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