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
                stage("OWASP Dependency Check"){
                    steps{
                            dependencyCheck additionalArguments: '''
                                --scan \'./\'
                                --out \'./\'
                                --format \'ALL\'
                                --prettyPrint''', odcInstallation: 'OWASP-DepCheck-10'
                        }

                stage("NPM Dependency Audit"){
                steps {sh 'npm audit --audit-level=critical'}
                 }
         
                }}
    }

}