pipeline {
    agent any
    stages {
        stage('Compile Code') {
            steps {
                sh 'mvn clean compile -e'
            }
        }
        stage('Test Code') {
            steps {              
                sh 'mvn clean test -e'
            }
        }
        stage('Jar ') {
            steps {               
                sh 'mvn clean package -e'
            }
        }
        stage('SonarQube analysis') {
           steps {
             withSonarQubeEnv(installationName: 'sonar') { 
             sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
             }
          }
        }
        stage('Upload Nexus') {
            steps {               
                nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.2']]]
            }
        }  
      


        
        
    }
}
