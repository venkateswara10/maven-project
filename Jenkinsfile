node {
    stage('Continous Download')
    {
   // git 'https://github.com/AnupamaSoma/maven-project.git'
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AnupamaSoma/maven-project.git']]])
     }
     stage('Continous Build') {
        sh 'mvn package'
     }
     stage('Continous Deployment') {
         sh ''' scp /var/lib/jenkins/workspace/scripted_pipeline/webapp/target/webapp.war ubuntu@172.31.86.232:/var/lib/tomcat9/webapps/testing.war'''
      // deploy adapters: [tomcat9(credentialsId: '28d390da-bfb0-485a-93af-7930d55e94b6', path: '', url: 'http://172.31.86.232:8080')], contextPath: 'test', war: '**/*.war'
     }
     stage('Continous Testing') {
       git 'https://github.com/AnupamaSoma/FunctionalTesting.git'
       sh 'java -jar /var/lib/jenkins/workspace/scripted_pipeline/testing.jar'
     }
     stage('Continous Delivery') {
       deploy adapters: [tomcat9(credentialsId: '28d390da-bfb0-485a-93af-7930d55e94b6', path: '', url: 'http://172.31.86.232:8080')], contextPath: 'test', war: '**/*.war'
     }
     
     }
