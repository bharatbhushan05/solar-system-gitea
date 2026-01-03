pipeline {
    agent { label 'linux' }

    tools {
        nodejs 'nodejs-22-6-0'
    }

    stages {

        stage("Checking node version") {
            steps {
                sh '''
                    node -v
                    npm -v
                '''
            }
        }

        stage('Dependency Scanning') {
            parallel {

                stage("OWASP Dependency Check") {
                    steps {
                            dependencyCheck(
                                            odcInstallation: 'OWASP-DepCheck-10',
                                            nvdCredentialsId: 'nvd-api-key',
                                            additionalArguments: '''
                                                --scan ./
                                                --out dependency-check-report
                                                --format HTML
                                                --prettyPrint
                                            '''
)

                    }
                }

                stage("NPM Dependency Audit") {
                    steps {
                        sh 'npm audit --audit-level=critical'
                    }
                }

            }
        }

    }
}
