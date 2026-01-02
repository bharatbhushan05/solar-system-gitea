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
        
            steps("Currect working dir"{
                sh ' pwd '
                sh ' npm install --no-audit '
            }
        
         
    }

}