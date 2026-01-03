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
                        sh 'mkdir -p $WORKSPACE/dependency-check-report'

                        dependencyCheck(
                            odcInstallation: 'OWASP-DepCheck-10',
                            nvdCredentialsId: 'nvd-api-key',
                            additionalArguments: """
                                --scan $WORKSPACE
                                --out $WORKSPACE/dependency-check-report
                                --format ALL
                                --prettyPrint
                            """
                        )

                        dependencyCheckPublisher(
                            pattern: 'dependency-check-report/dependency-check-report.xml'
                        )

                        // Debug proof
                        sh 'ls -R $WORKSPACE/dependency-check-report'
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
