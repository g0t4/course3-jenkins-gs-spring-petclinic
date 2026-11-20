pipeline {
    agent any
    
    stages {
        stage("Checkout"){
            steps {
                git branch:'main', url: 'https://github.com/mampezzan/course3-jenkins-gs-spring-petclinic'
            }
        }
        stage("Build"){
            steps {
                sh './mvnw package'
            }
        }
        stage("Capture"){
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
                to: 'nobody@nowhere.com', 
                recipientProviders: [previous()], 
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }    
}


