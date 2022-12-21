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
            stage('Maven Build'){
                steps{
                    sh 'mvn clean install'
                }
            }
            stage('static code analysis'){
                steps{
                   script{
                   withSonarQubeEnv(credentialsId: 'sonar-api-key') {
                     sh 'mvn clean package sonar:sonar'
                   }
                }
            }
       }
       stage('Quality Gate status'){
           steps{
               script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api-key'
               }

           }
       }
       stage('upload war file to Nexus'){
           steps{
               script{
                 def readPomVersion = readMavenPom file: 'pom.xml'
                 nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: '/var/lib/jenkins/workspace/project/target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '44.197.199.29:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'demoapp-release', version: "${readPomVersion.version}"

              }
           }
       }
    }

}

