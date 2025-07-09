pipeline {
    agent any
    stages {
        stage('git code download') {
            steps {
                echo "downloading code from git"
                git branch: 'main', url: 'https://github.com/archiehemal/maven-jenkins7.git'
            }
        }
        stage('build') {
            steps {
                sh '''docker build -t archie24/tomcat:${BUILD_NUMBER} .
                      docker tag archie24/tomcat:${BUILD_NUMBER} archie24/tomcat:latest
                      docker push archieh24/tomcat:${BUILD_NUMBER}
                      docker push archie24/tomcat:latest'''
            }
        }
    }
}
