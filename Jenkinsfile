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
               pwsh(script: 'docker images -a')
               pwsh(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """)

            }
        }
        
    }
}
