node  {
    def app
    def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']
    try{
        stage('Clone repository') {
            /* Let's make sure we have the repository cloned to our workspace */
                checkout scm
            }
        stage('Initialize'){
                def dockerHome = tool 'myDocker'
                env.PATH = "${dockerHome}/bin:${env.PATH}"
            }
        stage('Setting the variables values') {
            steps {
                 sh '''
                    #!/bin/bash
                    echo "$USER"
                 '''
            }
        }
        stage('Build image') {
            /* This builds the actual image; synonymous to
             * docker build on the command line */
                app = docker.build("rufatvalizadeh/helloworld")
            }
        stage('Push image') {
            /* Finally, we'll push the image with two tags:
             * First, the incremental build number from Jenkins
             * Second, the 'latest' tag.
             * Pushing multiple tags is cheap, as all the layers are reused. */
            docker.withRegistry('', 'dockerhub') {
                app.push("latest")
          } 
        }
        stage('Restart Application') {
                sh "docker-compose down"
                sh "docker-compose up -d"
        }
    }
    catch(e){
                slackSend channel: 'U03JF5TFX52',
                    color: 'danger',
                    tokenCredentialId:'slack-token',
                    message: "*ERROR:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n Description : ${e}\n More info at: ${env.BUILD_URL}"
    
    }
}