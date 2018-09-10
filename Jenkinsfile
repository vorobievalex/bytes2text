pipeline {
    agent { label '64-bit&&Docker' }

    options {
        timeout(time: 1, unit: 'HOURS')
        ansiColor('xterm')
        timestamps()
    }

    stages {
        stage('Build') {
            steps {
                git 'git@github.com:ReactiveX/RxCpp.git'
                sh 'make'
            }
        }
        post {
            always {
                archiveArtifacts allowEmptyArchive: true, artifacts: ''
            }
        }
    }
}
