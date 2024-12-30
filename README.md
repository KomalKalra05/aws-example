*<user password="1234" roles="manager-gui" username="admin"/>*
user 

FROM nginx:alpine

COPY . /usr/share/nginx/html


sudo docker build -t myweb

sudo docker run -d -p 80:80 myweb


FROM tomcat:9-jdk11

COPY target/*.war /usr/share/local/tomcat/webapps/

sudo docker build -t maven-web

sudo docker run -d -p 9090:8080 maven-web


pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
    }
    stages {
        stage('git repo & clean') {
            steps {
                bat "rmdir /s /q maven-se"
                bat "git clone https://github.com/KomalKalra05/maven-se.git"
                bat "mvn clean -f maven-se"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f maven-se"
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f maven-se"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f maven-se"
            }
        }
    }
}
