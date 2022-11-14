pipeline {
    agent any
   
    stages {
        stage ('GIT') {
            steps {
                git branch : 'adhir',
                url :'https://github.com/Dhekra-Ama/DevOps.git'
               
            }
           
    }
         stage('MVN COMPILE') {
                steps {
                    sh 'mvn clean compile'
                   
                }
               
            }
       stage('NVM CLEAN'){
                steps{
                    sh 'mvn clean package'
                   
                }
               
            }
        stage('MVN SONAREQUBE') {
            steps {
                sh'mvn sonar:sonar -Dsonar.login=e207d13a046afecedede67136a2a066c67249ede'
                }
           
        }
        stage('testing') {
        steps{
            sh'mvn test'
        }
        post {
            always {
            junit testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true
        }
        }
         
        }
   
       stage('nexus deploy') {
        steps{
            sh'mvn deploy '
           
        }
       
       }
       stage('DOCKER BUILD IMG STAGE'){
                steps{
                    script{
                        sh 'docker build -t achat-1.0-s7 .'
                    }
                   
                }
               
            }
      stage('DOCKER PUSH IMG STAGE '){
                steps{
                    script{
                        withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u madhir -p ${dockerhubpwd}'
                             }
                        sh 'docker tag  achat-1.0-s7 madhir/achat-1.0-s7:latest'     
                        sh 'docker push madhir/achat-1.0-s7'     
                    }
                   
                }
               
            }

       stage('Docker compose') {

                          steps {
                               sh 'docker-compose up -d '
                                 }  }
                                 stage('Email') {
        steps{
            mail bcc: '',
            body: 'Heyy , i am done working ',
            cc: '', from: '',
            replyTo: '', subject: 'The pipeline is done working here ...',
            to: 'adhir.maalaoui@esprit.tn'
        }
        }
    }
}
