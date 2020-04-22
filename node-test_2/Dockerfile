FROM node:alpine

COPY . /home/app
RUN cd /home/app && npm install
WORKDIR /home/app
CMD ['npm', 'start']