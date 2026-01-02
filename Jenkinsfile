pipeline{
    agent any
    tools{
        nodejs 'nodejs-22-6-0'
    }

    stages 
    {
        stage("Installing nodejs on agent"){
            steps{
                sh '''
                node -v
                npm -v
                '''
            }
        }
         
    }

}