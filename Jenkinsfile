node {
    stage('continous Download-git') {
    git 'https://github.com/AnupamaSoma/maven-project.git'
}
    stage('continous build-mvn'){
        sh 'mvn package'
    }
    stage('continous deployment'){
        deploy adapters: [tomcat8(credentialsId: 'mycred', path: '', url: 'http://172.31.81.254:8080')], contextPath: 'qaapp', war: '**/*.war'
    }
    stage('continous testing'){
        git 'https://github.com/AnupamaSoma/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/sp/testing.jar'
    }
    stage('continous deployment')
    {
        deploy adapters: [tomcat8(credentialsId: 'mycred', path: '', url: 'http://172.31.29.52:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
    stage('email notification')
    {
        mail bcc: '', body: '''hello
job is build successfully''', cc: '', from: '', replyTo: '', subject: 'jenkins-job', to: 'priyanjali.soma@gmail.com'
    }
}
