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
                sh '''docker build -t archiehemal/tomcat:${BUILD_NUMBER} .
                      docker tag archiehemal/tomcat:${BUILD_NUMBER} archiehemal/tomcat:latest
                      docker push archiehemal/tomcat:${BUILD_NUMBER}
                      docker push archiehemal/tomcat:latest'''
            }
        }
    }
}
