pipeline {
    agent any
    tools{
        jdk 'java17'
        maven 'maven3'
    }
    stages {
        stage('git code download') {
            steps {
                echo "downloading code from git"
                git branch: 'main', url: 'https://github.com/archiehemal/maven-jenkins7.git'
            }
        }
        stage('build') {
            steps {
                echo "build java project"
                sh 'mvn clean package'
            }
        }
        stage('Archive Artifacts') {
            steps {
                echo "archiving artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('trigger deployment') {
            steps {
                echo "trigered"
                build wait: false, job: 'deploy-pipeline'
            }
        }
    }
}




pipeline {
    agent any
    stages {
        stage('copy') {
            steps {
                copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'build-pipeline', selector: lastSuccessful()
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatcred', path: '', url: 'http://34.72.82.19:8090/')], contextPath: null, war: '**/*.war'
            }
        }
        }
    }
