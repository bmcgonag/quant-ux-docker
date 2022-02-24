FROM openjdk:19-jdk-bullseye

RUN mkdir -p /usr/src/quant-be

COPY . /usr/src/quant-be 

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

ENV TZ=America/Chicago

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /usr/src/quant-be

## Set ENV vars here
ENV QUX_HTTP_HOST=quant.example.com \
    QUX_HTTP_PORT=8080 \
    QUX_MONGO_DB_NAME=quantux \
    QUX_MONGO_TABLE_PREFIX=quantux \
    QUX_MONGO_CONNECTION_STRING=mongodb://mongo:27017 \
    QUX_MAIL_USER=mail_admin@example.com \
    QUX_MAIL_PASSWORD=some-strong-password0! \
    QUX_MAIL_HOST=mail.example.com \
    QUX_JWT_PASSWORD=some-log-string-of-randomized-numbers-characters \
    QUX_IMAGE_FOLDER_USER=/qux-images \
    QUX_IMAGE_FOLDER_APPS=/qux-image-apps

## Clone Quant-ux backend repo with pre-built java backend
RUN git clone https://github.com/KlausSchaefers/qux-java.git

## Run the java backend with this
CMD [ "java", "-jar",  "qux-java/release/qux-server.jar", "-Xmx2g", "-conf", "qux-java/matc.conf", "-instances 1" ]
