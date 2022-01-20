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
        stage('Run') {
            steps {
                script {
                    dir("C:/Users/jjcha/Documents/Diplomado/Repos/ejemplo-maven"){
                        sh "nohup bash mvnw spring-boot:run &"
                    }
                }
            }
        }
        stage('Wait') {
            steps {
                echo "Sleep 30 seconds"
                sleep(time: 30, unit: "SECONDS")
            }
        }
        stage('Curl') {
            steps {
                script {
                    dir("C:/Users/jjcha/Documents/Diplomado/Repos/ejemplo-maven"){
                        sh "curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'"
                    }
                }
            }
        }
    }
}

