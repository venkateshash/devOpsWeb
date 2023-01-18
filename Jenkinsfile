pipeline {
    agent any
    tools{
        maven 'maven_home'
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
        
                    steps{
                       deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://localhost:9090/')], contextPath: null, war: '**/*.war'
                    }
         }
    }
}
