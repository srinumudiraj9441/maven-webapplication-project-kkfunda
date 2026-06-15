pipeline {

    agent any

    tools {
        maven "maven-3.9.9"
    }

    stages {

        stage('Checkout Code') {

            steps {

                git branch: 'prod_DL',
                    url: 'https://github.com/srinumudiraj9441/maven-webapplication-project-kkfunda.git'
            }
        }


        stage('Build') {

            steps {

                sh "mvn clean package"
            }
        }


        stage('SonarQube Analysis') {

            steps {

                sh "mvn sonar:sonar"
            }
        }


        stage('Artifact Backup') {

            steps {

                sh "mvn deploy"
            }
        }


        stage('Deploy to Tomcat') {

            steps {

                sh '''
                curl -u admin:srinivas \
                --upload-file target/maven-web-application.war \
                "http://18.61.229.146:8080/manager/text/deploy?path=/maven-web-application&update=true"
                '''
            }
        }

    }
}
