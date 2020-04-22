FROM alpine AS builder
WORKDIR /home/app
RUN apk add --no-cache --update nodejs nodejs-npm
COPY package.json package-lock.json ./
RUN npm install --production

FROM alpine
WORKDIR /home/app
RUN apk add --no-cache --update nodejs nodejs-npm
COPY --from=builder /usr/src/app/node_modules ./node_modules
COPY . .
CMD [ 'npm', 'start' ]
