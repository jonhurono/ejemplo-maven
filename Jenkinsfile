pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                script {
                    dir("C:/Users/jjcha/Documents/Diplomado/Repos/ejemplo-maven"){
                        sh "mvn clean compile -e"
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dir("C:/Users/jjcha/Documents/Diplomado/Repos/ejemplo-maven"){
                        sh "mvn clean test -e"
                    }
                }
            }
        }
        stage('Jar') {
            steps {
                script {
                    dir("C:/Users/jjcha/Documents/Diplomado/Repos/ejemplo-maven"){
                        sh "mvn clean package -e"
                    }
                }
            }
        }
        stage('SonarQube analysis') {
            steps {
                script {
                // requires SonarQube Scanner 2.8+
                scannerHome = tool 'sonar-scanner'
                }
                withSonarQubeEnv('Sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.java.binaries=build"
                }
            }
        }
        stage('uploadNexus'){
            steps {
                script {
                    curl -X GET -u 'developer:developer' https://2613-207-248-201-48.ngrok.io/#admin/repository/test-nexus/com/devopsusach2020/DevOpsUsach2020/0.0.1/DevOpsUsach2020-0.0.1.jar -O
ls -ltr
                }
            }
        }
        
    }
}

