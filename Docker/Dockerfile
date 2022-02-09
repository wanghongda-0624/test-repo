FROM nginx:latest

#copy your web site files to nginx root directory
RUN chmod -R 775 /var
RUN chmod -R 775 /etc

#COPY $(Build.ArtifactStagingDirectory)/www/dist/ /usr/share/nginx/html/
COPY dist/ /usr/share/nginx/html/
COPY Docker/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
