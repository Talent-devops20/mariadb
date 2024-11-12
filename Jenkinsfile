pipeline {
    
        agent any
   
    stages {
        stage('git clone ') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-ssh-key', url: 'git@github.com:Talent-devops20/mariadb.git']])
            }
        }
        stage('helm version ') {
            steps {
               sh 'helm version'
            }
        }
        stage('deployment ') {
            steps {
               sh 'helm upgrade --install mariadb-deploy $WORKSPACE --values $WORKSPACE/prod-mariadb.yaml'
            }
        }
        
        stage('status ') {
             
            steps {
               sh 'helm list'
            }
        }
        stage('pod status ') {
             
            steps {
               sh 'kubectl get pod '
            }
        }
        
    }
    post{
        always{
            emailext body: '''Hi,

     The jenkins has been failed . please check it.

     Thanks
     Devops Team''', subject: 'testing jenkins pipeline: $JOB_URL', to: 'malleshdevops2021@outlook.com'
    }
    }
}
