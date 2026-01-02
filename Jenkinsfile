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
        }
         
    }


}