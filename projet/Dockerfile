FROM nimmis/alpine-apache
RUN apk update; \
    apk upgrade;

COPY projet/site/ /web/html/ 
EXPOSE 80