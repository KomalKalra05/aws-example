*<user password="1234" roles="manager-gui" username="admin"/>*
user 

FROM nginx:alpine
COPY . /usr/share/nginx/html
