FROM swr.cn-east-3.myhuaweicloud.com/cdo-org/nginx:latest

#copy your web site files to nginx root directory
RUN chmod -R 775 /var
RUN chmod -R 775 /etc

COPY dist/ /usr/share/nginx/html/
COPY docker/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
