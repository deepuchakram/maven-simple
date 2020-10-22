pipeline { 
    agent any
    tools {
        maven 'Maven'
    }
        stages { 
           stage('SCM Checkout') { 
               steps { 
                   git url:'https://github.com/deepuchakram/maven-simple.git' 
                       } 
                               } 
           stage('Build') { 
               steps { 
                        shell "mvn clean package"
                            } 
                    } 
           stage('Build Analysis') { 
               steps { 
                   withSonarQubeEnv('sonar')   
                          { 
                        shell "mvn sonar:sonar" 
                             } 
                    } 
                } 
          /* stage("Quality Gate") { 
               steps { 
                  timeout(time: 50, unit: 'MINUTES') { 
                     waitForQualityGate abortPipeline: true 
                       } 
                  } 
              } */ 
           stage('Deploy') { 
               steps { 
                   shell "mvn clean deploy " 
                             } 
                    } 
           //stage('Release') { 
               //steps { 
                  // shell "export JENKINS_NODE_COOKIE=dontKillMe; nohup java -jar $WORKSPACE/target/*.jar &" 
                    //       } 
                 //   } 
                } 
            } 

