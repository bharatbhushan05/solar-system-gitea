pipeline{
    agent any
    // tools{
    //     nodejs "node"
    // }

    stages {
        stage("Cloning git code to workplace"){
            steps{
                git branch: 'feature/enabling-cicd', url: 'https://github.com/bharatbhushan05/solar-system-gitea.git'
            
            }
        stage("Installing nodejs on agent"){
            steps{
                sh ```
                sudo apt update
                sudo apt install nodejs npm -y
                node -v
                npm -v
                ```
            }
        }
        }
         
    }


}