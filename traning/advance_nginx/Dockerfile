FROM nginx:latest

#Make sute we full up to date
RUN apt-get update -q && \
    apt-get dist-upgrade -y

#Remove the default configuration
RUN rm /etc/nginx/conf.d/default.conf

#Create our website's directory and make sure
#that the webserver process can read it
RUN mkdir -p /srv/www/html && \
    chown nginx:nginx /srv/www/html/

#Put out custum server configuration in
COPY nginx_main_site.conf /etc/nginx/conf.d/

#Copy out test file in then location that is eing servered up
COPY test.txt /srv/www/html/