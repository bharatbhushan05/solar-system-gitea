pipeline{
    agent any
    tools{
        nodejs 'nodejs-22-6-0'
  }
    triggers {
        githubPush()
    }
    stages {


         stage("Checking node version"){
            steps{
                sh '''
                    node -v
                    npm -v
                '''
            }
        }

        stage('Dependency Scanning'){
            parallel {
                stage("Currect working dir"){
                    steps{
                        sh 'pwd && ls -lrt'
                        sh 'npm install --no-audit'
                        }
                        }
                stage("NPM Dependency Audit"){
                steps {sh 'npm audit --audit-level=critical'}
                 }
         
                }}
    }

}