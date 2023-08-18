pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deploy'){
            steps{
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

// node {
//     def dockerImage = 'node:16-buster-slim'

//     stage('Build') {
//         docker.image(dockerImage).inside("-p 3000:3000") {
//             sh 'npm install'
//         }
//     }

//     stage('Test') {
//         docker.image(dockerImage).inside {
//             sh './jenkins/scripts/test.sh'
//         }
//     }

//     stage('Deploy!'){
//         docker.image(dockerImage).inside {
//             sh './jenkins/scripts/deliver.sh'
//             input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
//             sh './jenkins/scripts/kill.sh'
//         }
//     }
// }

