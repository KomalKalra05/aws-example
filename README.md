*<user password="1234" roles="manager-gui" username="admin"/>*
user 

FROM nginx:alpine

COPY . /usr/share/nginx/html


sudo docker build -t myweb

sudo docker run -d -p 80:80 myweb


FROM tomcat:9-jdk11

COPY target/*.war /usr/share/local/tomcat/webapps/
