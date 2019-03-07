FROM node:latest
MAINTAINER Marcel Rebello "mmprebello@gmail.com

#DEFINE PROXY TO DOWNLOAD PACKAGES
ARG proxy_now=http://myproxyserver.here.local:3128
ARG http_proxy=${proxy_now}
ARG https_proxy=${proxy_now}

ARG REPO="https://github.com/mprebello/system-managment-tape"
ARG SRC_APP="/usr/src/app"
ARG DST_APP="/usr/tapesystem"

ARG SRC_FRONTEND="${SRC_APP}/code/FrontEnd"
ARG SRC_BACKEND="${SRC_APP}/code/BackEnd"
ARG DST_FRONTEND="${DST_APP}/FrontEnd"
ARG DST_BACKEND="${DST_APP}/BackEnd"
ARG CONF_FRONTEND="conf/FrontEnd"
ARG CONF_BACKEND="conf/BackEnd"


RUN git clone $REPO $SRC_APP

RUN npm config set proxy ${http_proxy} && \
    npm config set https-proxy ${http_proxy} &&\
    npm config set strict-ssl false && \
    npm config set registry "http://registry.npmjs.org/"

RUN mkdir -p ${DST_BACKEND}
RUN cp ${SRC_BACKEND}/package.json ${DST_BACKEND}
RUN cd ${DST_BACKEND} && npm install -g

RUN mkdir -p ${DST_FRONTEND}
RUN cp $SRC_FRONTEND/package.json ${DST_FRONTEND}
RUN cd ${DST_FRONTEND} && npm install -g

COPY init/* /
COPY conf /

RUN cp -ar ${SRC_BACKEND}/* ${DST_BACKEND}/
RUN cp -ar ${SRC_FRONTEND}/* ${DST_FRONTEND}/

COPY init/* /
RUN mkdir /conf
COPY conf/ /conf/
RUN mv ${CONF_FRONTEND}/* ${DST_FRONTEND}/config/
RUN mv ${CONF_BACKEND}/* ${DST_BACKEND}/config/

RUN chmod 755 /entrypoints.sh

EXPOSE 3000

ENTRYPOINT ["/entrypoints.sh"]
#CMD [ "/usr/sbin/apache2ctl", "-D" , "FOREGROUND" ]
