pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Aziz20guizani/DevOps-ProjetStudentsManagement.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean verify -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                        sh '''
                            mvn sonar:sonar \
                              -Dsonar.projectKey=DevOps-ProjetStudentsManagement \
                              -Dsonar.projectName=DevOps-ProjetStudentsManagement \
                              -Dsonar.host.url=http://192.168.50.4:9000 \
                              -Dsonar.token=$SONAR_TOKEN
                        '''
                    }
                }
            }
        }
    }
}

