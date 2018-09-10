pipeline {
    agent { label '64-bit&&Docker' }

    options {
        timeout(time: 1, unit: 'HOURS')
        timestamps()
    }

    stages {
        stage('Build') {
            steps {
                dir('RxCpp') {
                    checkout([$class: 'GitSCM',
                              branches: [[name: '*/master']],
                              doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: false]], submoduleCfg: [],
                              userRemoteConfigs: [[url: 'git@github.com:ReactiveX/RxCpp.git']]
                    ])
                }
                sh 'rm -f bytes2text'
                gcc_container 'make'
                // TODO: verification
            }
        }
    }
    post {
        always {
            archiveArtifacts allowEmptyArchive: true, artifacts: 'bytes2text'
        }
    }
}


def gcc_container(String command) {
    sh "docker run --rm -v ${pwd()}:/usr/src/myapp -w /usr/src/myapp gcc:4.9 ${command}"
}
