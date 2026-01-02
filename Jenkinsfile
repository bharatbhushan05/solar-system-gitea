pipeline{
    agent any
    // tools{
    //     nodejs "node"
    // }

    stages 
    {
        stage("Installing nodejs on agent"){
            steps{
                sh '''
                sudo apt update
                sudo apt install nodejs npm -y
                node -v
                npm -v
                '''
            }
        }
         
    }

}