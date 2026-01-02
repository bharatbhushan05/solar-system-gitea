pipeline{
    agent any
    tools{
        nodejs 'nodejs-22-6-0'
    }

    stages 
    {
        stage("Checking node version"){
            steps{
                sh '''
                node -v
                npm -v
                '''
            }
        }
        stage{
            steps{
                sh ' pwd '
                sh ' npm install --no-audit '
            }
        }
         
    }

}