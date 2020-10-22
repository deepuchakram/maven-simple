pipeline {

    agent any

    tools { 

        maven 'Maven' 

        jdk 'Jdk8' 

    }

    stages {
           stage('Code Checkout') {

            steps {
         
            git credentialsId: 'deepuchakram', url: 'https://github.com/deepuchakram/maven-simple.git'
           }           
        }
        
        stage('Code Analysis') {

           steps {

              withSonarQubeEnv('Code QualityAnalysis') {

                sh 'mvn sonar:sonar'

              }

            }          
	}

       stage("Quality Gate") {

            steps {

              timeout(time: 1, unit: 'HOURS') {

                waitForQualityGate abortPipeline: true

              }

            }

         }
           
        stage('Build & Unit test') {
       		
	steps {
               
               echo "Building maven-simple Application"

                sh "mvn -version"

                sh "mvn clean install -f pom.xml"
	}
            }

            post {

                success {

                    junit 'target/surefire-reports/**/*.xml' 

                }

            }

        }
