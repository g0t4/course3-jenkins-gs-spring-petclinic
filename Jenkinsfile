pipeline {
    agent any

      stages{
        stage("build"){
            steps {
                bat "./mvnw.cmd package"
            }
        }
        stage("capture"){
            steps {
             archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
            jacoco()
            junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'   
            }
        }
    }
}
