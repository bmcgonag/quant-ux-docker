FROM node:16-alpine

# install git
RUN apk --no-cache add git

# install bash
RUN apk --no-cache add bash

RUN apk --no-cache add build-base

# Install make
RUN apk --no-cache add make

# Install python/pip
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
#RUN python3 -m ensurepip
#RUN pip3 install --no-cache --upgrade pip setuptools

RUN mkdir -p /usr/src/quant-ux

WORKDIR /usr/src/quant-ux

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

ENV TZ=America/Chicago

## Set ENV vars here
ENV QUX_PROXY_URL=http://qux-be.quantux.com:8080

## Clone the frontend repo
RUN git clone https://github.com/KlausSchaefers/quant-ux.git

RUN cd quant-ux && npm install && npm run build

RUN cd

# Expose the Web Port
EXPOSE 8082

## Start the server running
CMD [ "node", "quant-ux/server/start.js" ]
