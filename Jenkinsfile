pipeline{
    agent any
    tools{
      maven "maven3.8.6"    
    }
    stages{
        stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
        git credentialsId: 'GitHubcredentials', url: 'https://github.com/Neizeen2022/GTBank-app.git'
      }    
    }
    stage('2Test&Buils'){
        steps{
            sh "echo 'running Junit-test-cases' "
            sh "echo 'testing must pass to create artifacts' "
            sh "mvn clean package"
        }
    }
    stage('3CodeQuality'){
        steps{
            sh "echo 'Performing Code Quality Analysis with sonarqube' "
            sh "mvn sonar:sonar"
        }
    }
    stage('4uploadArtifact'){
        steps{
            sh " echo 'uploading Artifacts to nexus' "
            sh "mvn deploy"
        }    
    }
    stage('5Deploy2Prod'){
        steps{
            sh "echo 'Deploying to Production' "
            deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://3.87.203.82:8080/')], contextPath: null, war: 'target/*war'
        }
    }
    }
}
