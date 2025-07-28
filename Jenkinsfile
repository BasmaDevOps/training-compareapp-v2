pipeline {
    agent any
    stages {
        //Continuous Integration
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
                //Continuous Delivery
        stage('Docker Build&Push') {
            steps {
                withDockerRegistry(credentialsId: 'docker', url: "") {
                    sh 'docker build -t basmadevops/compare-appt2025 .'
                    sh 'docker push basmadevops/compare-appt2025'
                }
            }
        }
        //Continuous Deployment
        stage('Deploy') {
            steps {
                withDockerRegistry(credentialsId: 'docker', url: "") {
                    sh 'docker -H ssh://ubuntu@13.39.20.51 run -d --name myapp -p 8083:8080 basmadevops/compare-appt2025'
                }
            }  
        }
    }
}
