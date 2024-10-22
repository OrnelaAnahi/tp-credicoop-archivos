pipeline {
    agent any
    tools {
        maven 'MavenOtro' 
    }
    environment {
      WORK_DIR_VM2 = '/home/user/dds-deploy'
    }
    
    stages {
        stage('checkout') {
            steps {
                echo 'checking out SCM Jobs Project'
                    git(
                        branch: 'main', 
                        credentialsId: 'credencialGitHub', 
                        url: 'https://github.com/OrnelaAnahiLugo/dds-deploy.git'
                    )
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
       stage('SonarQube analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner';  
                    withSonarQubeEnv(credentialsId: 'tokenSonarQube', installationName: 'sonarQube') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=ibisoft-arg_devops-credi \
                        -Dsonar.sources=src/main/java \
                        -Dsonar.projectBaseDir=./ \
                        -Dsonar.java.binaries=target/classes \
                        -Dsonar.webhooks.project=http://192.168.159.130:8080/sonarqube-webhook/
                        """
                   
                    }
            }
        }
           
       }
       stage('Quality Gate') {
            steps {
                script {
                    sleep(10) // Espera inicial
                    def qualitygate = waitForQualityGate()
                    // Verificar si la tarea está en progreso
                    while (qualitygate.status == "IN_PROGRESS") {
                        echo "SonarQube task '${qualitygate.taskId}' is still in progress. Waiting..."
                        sleep(10) // Espera antes de volver a comprobar el estado
                        qualitygate = waitForQualityGate() // Revisa el estado nuevamente
                    }
                    // Verificar el resultado final de la puerta de calidad
                    if (qualitygate.status != "OK") {
                        echo "Quality Gate failed. Status: ${qualitygate.status}"
                        error 'Stopping the pipeline due to failed Quality Gate'
                    } else {
                        echo 'Quality Gate passed!'
                    }
                }
            }
        }
        stage("Deploy to Minikube"){
            agent { label 'minikube' }
            steps{
                sh 'minikube start'
                sh 'kubectl config use-context minikube'
                dir("${WORK_DIR_VM2}"){
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl rollout status deployment/app-libros'
                    sh ' kubectl get pods'

                }
                echo 'Deployment complete!'
            }
            
        }
    }

}
