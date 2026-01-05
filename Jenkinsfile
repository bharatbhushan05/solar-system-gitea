pipeline {
    agent any             // { label 'linux' }
    tools {
        nodejs 'nodejs-22-6-0'
    }
    stages {

        stage('Verify Node and NPM Version') {
            steps {
                sh 'node --version'
                sh 'npm --version'
            }
        }
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
                       // dependencyCheckPublisher( failedTotalCriticalVulnerabilities: 1, pattern: 'dependency-check-report/dependency-check-report.html')
                       // junit allowEmptyResults: true, stdioRetention: '', testResults: 'dependency-check-junit.xml'
                        
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
        stage('Unit Testing') {
            options {retry(2) }
            steps {
                withcredentials([usernamePassword(credentialsId: 'mongo-db-credentials', usernameVariable: 'NPM_USERNAME', passwordVariable: 'NPM_PASSWORD')]) {
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        }
        stage('Verify Node and NPM Version') {
            steps {
                sh 'node --version'
                sh 'npm --version'
            }
        }
    }
}