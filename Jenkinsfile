pipeline {
    agent any
    stages {
            stage("checkout") {
                steps {
                    git branch:'main', url: 'https://github.com/g0t4/course3-jenkins-gs-spring-petclinic'    
                }
            }
            stage("buiild") {
                steps {
                    sh "./mvnw package"
                }
            }
            stage("capture") {
                //**/target/*.jar
                steps {
                    archiveArtifacts artifacts: '**/target/*.jar'
                    jacoco()
                    junit '**/target/surefire-reports/TEST*.xml'
                }
            }
    }
    //Post snippet here
    
    post {
        always {
            emailext to: 'always@foo.com',recipientProviders: [previous()],
                    subject: "${currentBuild.currentResult} : Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "{env.BUILD_URL}\n${currentBuild.absoluteUrl}"
            }
    }
    
}