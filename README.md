copy_script.sh;
#!/bin/sh

cp /app/target/*.war /target/ && echo "WAR files copied to /target in host"


first docker file;

FROM maven:3.6.3-openjdk-8

WORKDIR /app

COPY . .

RUN mvn clean install

COPY copy_script.sh /copy_script.sh

RUN chmod +x /copy_script.sh

ENTRYPOINT ["/copy_script.sh"]

docker run commands;

docker run --rm -v $(pwd)/target:/target lavagna-builder
