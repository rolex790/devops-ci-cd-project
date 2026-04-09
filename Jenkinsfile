pipeline {
    agent any
    
    triggers {
        githubPush()
    }

    tools {
        jdk 'JDK'
        maven 'Maven'
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rolex790/devops-ci-cd-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                cp target/myapp.war /opt/apache-tomcat-9.0.116/webapps/
                '''
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESS - APP DEPLOYED 🚀'
        }
        failure {
            echo 'BUILD FAILED ❌'
        }
    }
}
