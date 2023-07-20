node{
   stage('SCM Checkout'){
     git 'https://github.com/prithivisp23/Project0306.git'
   }
stage('warfilebuild'){

      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
   stage('SonarQube Analysis') {
	        def mvnHome =  tool name: 'maven3', type: 'maven'
	        withSonarQubeEnv('prithividevOpsProjectsonarqube') { 
	          sh "${mvnHome}/bin/mvn sonar:sonar"
	        }
	    }
stage('Build Docker Image'){
   sh 'docker build -t prithivisp23/myweb:0.0.2 .'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]) {
   sh "docker login -u prithivisp23 -p ${dockerPassword}"
    }
   sh 'docker push prithivisp23/myweb:0.0.2'
   }
   stage('Remove Previous Container'){
	try{
		sh 'docker rm -f tomcattest'
	}catch(error){
		//  do nothing if there is an exception
	}
}
   stage('Nexus Image Push'){
   sh "docker login -u admin -p admin123 3.110.218.160:8083"
   sh "docker tag prithivisp23/myweb:0.0.2 3.110.218.160:8083/prithivi:1.0.0"
   sh 'docker push 3.110.218.160:8083/prithivi:1.0.0'
   }
   stage('Docker deployment'){
   sh 'docker run -d -p 8090:8080 --name tomcattest prithivisp23/myweb:0.0.2' 
   }
}
