pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
               sh label: '', script: 'ssh -tt -i /var/jenkins_home/.ssh/id_rsa root@172.17.0.1 "cd /home/ec2-user/github_repos/azure-voting-app-redis/azure-vote/ && docker images -a && docker build -t jenkins-pipeline . && docker images -a && cd .."'
            }
      }
      stage('Start test app') {
         steps {
            sh label: '', script: 'ssh -tt -i /var/jenkins_home/.ssh/id_rsa root@172.17.0.1 "cd /home/ec2-user/github_repos/azure-voting-app-redis && docker-compose up -d "'
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh label: '', script: 'ssh -tt -i /var/jenkins_home/.ssh/id_rsa root@172.17.0.1 "pytest /home/ec2-user/github_repos/azure-voting-app-redis/tests/test_sample.py"'
         }
      }
      stage('Stop test app') {
         steps {
            sh label: '', script: 'ssh -tt -i /var/jenkins_home/.ssh/id_rsa root@172.17.0.1 "cd /home/ec2-user/github_repos/azure-voting-app-redis && docker-compose down"'
            }
      }
   }
}
