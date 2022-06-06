node  {
    def app
    def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']
    try{
        stage('Clone repository') {
            /* Let's make sure we have the repository cloned to our workspace */
                checkout scm
            }
       
    }
    catch(e){
                slackSend channel: '#yourchannel',
                    color: 'danger',
                    tokenCredentialId:'slackCredentials',
                    message: "*ERROR:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n Description : ${e}\n More info at: ${env.BUILD_URL}"
    
    }
}