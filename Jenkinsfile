node {
   
   stage('Code Checkout') { 
      git credentialsId: 'githubid', url: 'https://github.com/manjuorg/maven-examples.git'     
    }
   stage('Build') {
    withMaven(jdk: 'jdk-8', maven: 'MAVEN') {
      sh 'mvn clean compile'
      }
    }
   stage('Unit Test run') {
    withMaven(jdk: 'jdk-8', maven: 'MAVEN') {
     sh 'mvn test'
      } 
    }
   stage('sonarqube'){
   //withSonarQubeEnv(credentialsId: 'sonarid') {
    withMaven(jdk: 'jdk-8', maven: 'MAVEN') {
    sh 'mvn sonar:sonar -Dsonar.projectKey=maven-examp -Dsonar.organization=manjuorg -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=9d56ad4f78940bbe70bd9d8afad87704b59fb5ea' 
      }
    }
  stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
    }
   stage('Package to Jfrog') {
    withMaven(jdk: 'jdk-8', maven: 'MAVEN') {
     sh 'mvn package'
      }
    }
   
   stage('Deploy to Dev') {
     
    }
   stage('Automation Testing') {
     
    }
   stage('Deploy to Test') {
     
    }
   stage('Smoke Testing') {
     
    }
   stage('Deploy to Prod') {
     
    }
   stage('Acceptance Testing') {
     
    }
}
