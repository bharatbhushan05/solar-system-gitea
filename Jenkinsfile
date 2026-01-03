pipeline {
    agent { label 'linux' }

    options {
        skipDefaultCheckout()
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'feature/enabling-cicd',
                    url: 'https://github.com/bharatbhushan05/solar-system-gitea.git'
            }
        }

        stage('Verify Environment') {
            steps {
                sh '''
                  echo "Node:"
                  hostname
                  echo "User:"
                  whoami
                  echo "Git:"
                  which git
                  git --version
                '''
            }
        }

    }
}
