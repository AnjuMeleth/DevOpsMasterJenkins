pipeline{
    agent{label 'master'}
    tools{
        maven 'M3'
    }
    stages{
        stage('Checkout'){
            steps{
                git 'https://github.com/AnjuMeleth/spring-petclinic.git'
            }
        }
        stage('Build'){
            steps{
                 sh 'mvn clean compile'
            }
        }
        stage('Test'){
            steps{
                     sh 'mvn test'
                     junit '**/target/surefire-reports/TEST-*.xml'
            }
        }
        stage('Package'){
            steps{
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
        }
        stage('Reports'){
            steps{
                sh 'mvn verify'
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site/jacoco', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])     
                }
        }   
    }
}
