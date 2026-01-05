pipeline {
    agent any             // { label 'linux' }
    tools {
        nodejs 'nodejs-22-6-0'
    }
    stages {
        // check troubleshooting -> Troubleshooting 1. 
        // stage('Checkout on Linux Agent') {
        //     steps {
        //         git branch: 'feature/enabling-cicd',
        //             url: 'https://github.com/bharatbhushan05/solar-system-gitea.git'
        //     }
        // }
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
                    }
                }
                stage("NPM Dependency Audit and fixing it") {
                    steps {
                        script {
                            def auditStatus = sh(
                                script: 'npm audit --audit-level=critical',
                                returnStatus: true
                            )
                            sh 'npm audit fix --force'
                            if (auditStatus != 0) {
                                error("Critical vulnerabilities detected even after fix")
                            }
                        }
                    }
                }
            }
        }
    }
}