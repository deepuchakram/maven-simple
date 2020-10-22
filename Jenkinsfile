node('master') {
	stage ('checkout code'){
		https://github.com/deepuchakram/maven-simple.git
		
		 mvnHome = tool 'Maven'
	}
	
	stage ('Compile'){
		shell "mvn clean install -Dmaven.test.skip=true"
	} 
	
	stage ('Test Cases Execution'){
		shell "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}
	
	stage ('Sonar Analysis'){
		shell 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9005'
	}
		
	stage ('Build'){
		shell "mvn clean install package -Dmaven.test.skip=true"
	}
	
	stage ('Archive Artifacts'){
		//junit '**/target/surefire-reports/TEST-*.xml'
      //archiveArtifacts 'target/*.jar'
		//archiveArtifacts(artifacts: 'target/*.war', fingerprint: true) 
		shell "mvn insall tomcat7:deploy"
		//deploy adapters: [tomcat7(credentialsId: '8217496f-3b5c-4dab-9bdf-e30380271946', path: '', url: 'http://192.168.0.106:8086')], contextPath: 'rps', war: '*/*.war'
	}
	stage('Push to Nexus') {
      // Run the maven build
      //withEnv(["MVN_HOME=$mvnHome"]) {
         //if (isUnix()) {
           shell '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy'
         //} else {
            //bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean deploy/)
         //}
      //}
   }
	//Stage ('Upload war To Nexus'){
		
	//shell nexusArtifactUploader credentialsId: 'nexus', groupId: 'maven-build', nexusUrl: '192.168.0.106:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-build-snapshot', version: '1.0.0'

	//}	
	
	stage ('Deployment'){
		shell 'cp target/*.war /C:/Users/Apache Software Foundation/apache-tomcat-8.5.58/webapps'
	}
	stage ('Notification'){
		//slackSend color: 'good', message: 'Deployment Sucessful'
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "sudeepthi516@gmail.com"
		    )
	}
}