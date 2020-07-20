pipeline {
    agent any

    stages {
        stage('Hello Banner') {
            steps {
                echo 'This is my first scripted jenkins pipeline'
            }
        }   
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
               sh label: '', script: '''ssh -tt -i /var/jenkins_home/.ssh/id_rsa root@172.17.0.1
               cd /home/ec2-user/github_repos/azure-voting-app-redis/azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..'''
            }
        }
        
    }
}
