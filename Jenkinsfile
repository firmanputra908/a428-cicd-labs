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
//         stage('Deploy'){
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//                 input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
//                 sh './jenkins/scripts/kill.sh'
//             }
//         }
//     }
// }

node {
    def dockerImage = 'node:16-buster-slim'
    def dockerPort = '-p 3000:3000'

    stage('Build') {
        docker.image(dockerImage).inside(dockerPort) {
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image(dockerImage).inside {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval'){
        input message : 'Lanjutkan ke tahap Deploy?'
    }

    stage('Deploy'){
        docker.image(dockerImage).inside(dockerPort) {
            sh './jenkins/scripts/deliver.sh'
            echo 'Aplikasi berhasil di deploy, dan akan berjalan selama 60 menit,setelah itu akan mati'
            sleep time : 3600, unit: 'SECONDS'
            sh './jenkins/scripts/kill.sh'
        }
    }
}

