pipeline {
    agent any

    stages {
        stage('Check infra') {
            steps {
                
                
                    ansiblePlaybook credentialsId: 'local_key', installation: 'ansible', playbook: 'infra_check.yml'
                
                
                
            }
        }

        stage('Build image') {

            steps {
                
                withCredentials([
                    usernamePassword(credentialsId: 'docker-pass', usernameVariable: 'username', passwordVariable: 'password')
                ]){
                    ansiblePlaybook credentialsId: 'local_key', installation: 'ansible', playbook: 'eks_build_image.yml'
                }
                
                
            }
        }

        stage('Deploy to k8') {

            steps {
                
                withCredentials([
                    usernamePassword(credentialsId: 'docker-pass', usernameVariable: 'username', passwordVariable: 'password')
                ]){
                    ansiblePlaybook credentialsId: 'local_key', installation: 'ansible', playbook: 'kubernates_manage.yml'
                }
                
                
            }
        }
    }
}
