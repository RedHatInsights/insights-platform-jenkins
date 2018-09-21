def deploy (endpoint) {

    node {
        env.NODEJS_HOME = "${tool 'node-8'}"
        env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"

        checkout scm

        stage('deploy') {
            withCredentials(bindings: [sshUserPrivateKey(credentialsId: 'insightsbot',
                                                         keyFileVariable: 'insightsbot',
                                                         passphraseVariable: '',
                                                         usernameVariable: '')]) {

                sh '''
                    eval `ssh-agent`
                    ssh-add "$insightsbot"
                    rsync -arv -e "ssh -2" * sshacs@unprotected.upload.akamai.com:/114034/$endpoint
                '''
            }
        }
    }
}
