pipeline {
    agent any
    triggers {
        githubPush()
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('Dockerhub')
    }
    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }

        stage('Login to Dockerhub') {
            steps {
                withCredentials([string(credentialsId: 'Dockerhub', variable: 'DOCKERHUB_ACCESS_TOKEN')]) {
                    script {
                        sh "echo '${DOCKERHUB_ACCESS_TOKEN}' | docker login -u abodiaa --password-stdin"
                    }
                }
            }
        }

        stage('Pulling base image from Dockerhub') {
            steps {
                sh 'docker pull abodiaa/amf-base:latest'
            }
        }

        stage('docker build') {
            steps {
                sh(script: """
                    docker images -a
                    docker build -t abodiaa/5g-amf:latest . 
                    docker images -a
                """)
            }
        }

        stage('Scan Image for Common Vulnerabilities and Exposures') {
            steps {
                sh 'trivy image abodiaa/5g-amf --output trivy-report.json'
            }
        }

        stage('Pushing to Dockerhub') {
            steps {
                sh 'docker push abodiaa/5g-amf:latest'
            }
        }

        stage('Build and Package Helm Chart') {
            steps {
                sh 'helm package ./helm/'
            }
        }

        stage('Configure Kubernetes Context') {
            steps {
                sh 'aws eks --region us-east-1 update-kubeconfig --name 5G-Core-Net'
            }
        }

        stage('Deploy Helm Chart on EKS') {
            steps {
                sh 'helm upgrade --install amf ./helm/'
            }
        }
    }

    post {
        always {
            // Archiving Test Result
            archiveArtifacts artifacts: 'trivy-report.json', fingerprint: true
            sh 'docker rmi abodiaa/5g-amf'
            sh 'docker rmi abodiaa/amf-base'
        }
    }
}
