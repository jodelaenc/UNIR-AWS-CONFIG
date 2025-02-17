pipeline {
    agent any
    
    stages {
        stage('Get Code') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'UNIR', 
                                                 usernameVariable: 'GIT_USERNAME', 
                                                 passwordVariable: 'GIT_PASSWORD')]) {
                    git url: "https://$GIT_USERNAME:$GIT_PASSWORD@github.com/jodelaenc/UNIR-AWS-CONFIG.git", branch: 'staging'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    sam deploy --no-fail-on-empty-changeset --config-file samconfig.toml --config-env staging --force-upload
                '''
            }
        }
    }
}
