// pipeline {
//     agent {
//         docker {
//             image 'node:16-buster-slim' 
//             args '-p 3000:3000' 
//         }
//     }
//     stages {
//         stage('Build') { 
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//     }
// }

node {
    def dockerImage = 'node:16-buster-slim'

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        agent {
            docker {
                image dockerImage
                args '-p 3000:3000'
            }
        }
        steps {
            sh 'npm install'
        }
    }

    stage('Test') {
        agent any
        steps {
            script {
                sh './jenkins/scripts/test.sh'
            }
        }
    }
}
