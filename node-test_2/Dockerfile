FROM node:alpine

COPY . /home/app
RUN cd /home/app && npm install --production
WORKDIR /home/app
CMD ['npm', 'start']
