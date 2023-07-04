pipeline {
    agent any
    
    stages {
            
        stage("checkout") {
            steps {
                git branch:'main', url: 'https://github.com/g0t4/course3-jenkins-gs-spring-petclinic' 
            }
        }
    
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }
        
        stage("capture") {
            steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'
            }
        }
    }

    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
            	to: 'always@foo.bar', 
            	recipientProviders: [previous()], 
            	subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }

}