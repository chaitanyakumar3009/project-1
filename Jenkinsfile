pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/chaitanyakumar3009/project-1.git'
                }
            }
        }

        
    }
     stages {

        stage('Unit Test'){

            steps{

                script{

                    sh 'mvn test'
                }
            }
        }


    }

}