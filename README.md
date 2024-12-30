*<user password="1234" roles="manager-gui" username="admin"/>*
user 

FROM nginx:alpine

COPY . /usr/share/nginx/html


sudo docker build -t myweb

sudo docker run -d -p 80:80 myweb
