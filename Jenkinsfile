pipeline {
    agent { label 'Jenkins-agent' }
    tools {
       jdk 'java17'
       maven 'Maven3'
    }
stages {
    stage ("cleanup workspace"){
                steps {
                    cleanWs()
                }
    }
    stage ("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/jcbproject/test-ci-cd.git'
                }
    }
    stage ("Build Application"){
                 steps {
                    sh "mvn clean package"
                 }
    }
    stage ("Test Application"){
                 steps {
                    sh "mvn test"
                 }
     }
    stage ("SonarQube Analysis"){
                 steps {
                    script {
                        withSonarQubeEnv (credentialsId: 'jenkins-sonarqube-token'){
                            sh "mvn sonar:sonar"
                       }
                    }
                 }
    }
  }
}
