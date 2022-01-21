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
            steps{
                script{
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv('sonar-server') {
                    bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.sources=src -Dsonar.java.binaries=build"
                    }
                }
            }
        }
        
        stage('uploadNexus') {
            steps {
                echo 'uploadNexus'
                script {
                    nexusPublisher nexusInstanceId: 'nexus_rodrigo', nexusRepositoryId: 'test-repo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'C:/Users/jjcha/Documents/Diplomado/Repos/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
                }
            }
        }
        
    }
}