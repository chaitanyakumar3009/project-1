pipeline{

    agent any

       stages{
            stage('git checkout'){
               steps{
                    git branch: 'main', url: 'https://github.com/chaitanyakumar3009/project-1.git'
               }

            }
            stage('unit test'){
               steps{
                  sh 'mvn test'
               }
            }
            stage('Integration Testcase'){
               steps{
                  sh 'mvn verify  -DskipUnitTests'
               }
            }
       }

}

