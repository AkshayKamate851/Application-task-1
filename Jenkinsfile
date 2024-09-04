pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("my-app:latest")
                }
            }
        }
        stage('Deploy to S3') {
            steps {
                sh 'aws s3 cp my-app.zip s3://my-app-deployments/'
            }
        }
        stage('Deploy via CodeDeploy') {
            steps {
                script {
                    def deploy = step([
                        $class: 'AWSCodeDeployPublisher',
                        s3bucket: 'my-app-deployments',
                        applicationName: 'MyApp',
                        deploymentGroupName: 'MyDeploymentGroup'
                    ])
                }
            }
        }
    }
}

