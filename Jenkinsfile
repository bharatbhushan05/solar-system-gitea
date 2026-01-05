pipeline {
//   agent { label 'linux' }

    tools {
        nodejs 'nodejs-22-6-0'
    }

    stages {
        // check troubleshooting -> Troubleshooting 1. 
        stage('Checkout on Linux Agent') {
            steps {
                git branch: 'feature/enabling-cicd',
                    url: 'https://github.com/bharatbhushan05/solar-system-gitea.git'
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

                stage("NPM Dependency Audit and fixing it") {
                    steps {
                        sh 'npm audit --audit-level=critical'
                        sh 'npm audit fix'
                    }
                }

            }
        }

    }
}
