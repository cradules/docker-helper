FROM python:3

#Add some labels for cache bustin and annotating
LABEL version="1.0"
LABEL org.sgnn.name="python-webserver"

#Set a variable that we wil keep reusing to prevent typos
ENV SRV_PATH=/srv/www/html/

#Make sure we are fully up to date
RUN apt-get update -q && \
    apt-get dist-upgrade -y && \
    apt install net-tools

#Let DOcker know that the exposed port we will use is 8000
EXPOSE 8000

#Create our website's directory, then create the limited user
#and group
RUN mkdir -p $SRV_PATH && \
    groupadd -r -g 350 pythonsrv && \
    useradd -r -m -u 350 -g 350 pythonsrv

#Define ./external as an externally-monted directory
VOLUME [ "$SRV_PATH/external" ]
#To serve things up with Python, we need to be in that
#same directory
WORKDIR $SRV_PATH

#COpy out test file
COPY test.txt $SRV_PATH

#ADD a URL=hosted content into the image
ADD https://raw.githubusercontent.com/moby/moby/master/README.md  $SRV_PATH

#Make sure that we can read all of the files as a limited user
RUN chown -R pythonsrv:pythonsrv $SRV_PATH

#From here on out, use the limited user
USER pythonsrv

#Runthe simple httppython server to serve up the content
CMD [ "python3", "-m", "http.server" ]