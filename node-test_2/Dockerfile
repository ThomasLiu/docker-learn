FROM alpine:latest

RUN apk add --no-cache --update nodejs nodejs-npm
COPY . /home/app
RUN cd /home/app && npm install --production
WORKDIR /home/app
CMD ['npm', 'start']
