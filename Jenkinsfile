pipeline  {
    def app
    def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']
    stages{
        stage('Clone repository') {
            /* Let's make sure we have the repository cloned to our workspace */
                checkout scm
            }
       
    }
}