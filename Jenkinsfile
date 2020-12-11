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
        stage('Upload Nexus Dev2') {
            steps {               
                nexusPublisher nexusInstanceId: 'nexusdev2', nexusRepositoryId: 'test-repo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: '/Users/servidorcasa/Documents/Cursos/2020_devops/ejemplo_maven_24_11_2020/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
            }
        }  
      


        
        
    }
}
