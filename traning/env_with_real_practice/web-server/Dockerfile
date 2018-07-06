FROM nginx:latest
#Make sure we are fully up to date
RUN apt-get update -q && \
    apt-get dist-upgrade -y && \
    apt-get install openssl && \
    apt-get clean && \
    apt-get autoclean

# Setup any variables we need
ENV SRV_PATH /srv/www/html

#Get a variable defined for our password
ARG PASSWORD=test

#Remove default configuration
RUN rm /etc/nginx/conf.d/default.conf

#Change ownership of copied files
RUN mkdir -p ${SRV_PATH} && \
    chown nginx:nginx ${SRV_PATH}
#Setup auth file
RUN printf "user:$(openssl passwd -1 $PASSWORD)\n" >> ${SRV_PATH}/.httpasswd

#Add or own configuration
COPY nginx_main_site.conf /etc/nginx/conf.d/

