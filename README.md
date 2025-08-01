copy_script.sh;
#!/bin/sh

cp /app/target/*.war /target/ && echo "WAR files copied to /target in host"

java -Ddatasource.dialect=HSQLDB \
  "-Ddatasource.url=jdbc:hsqldb:file:/app/lavagna_db;shutdown=true" \
  -Ddatasource.username=sa \
  -Ddatasource.password= \
  -Dspring.profiles.active=dev \
  -jar /app/target/lavagna-jetty-console.war




  

first docker file;


FROM maven:3.6.3-openjdk-8

WORKDIR /app

COPY . .

RUN mvn clean install

COPY copy_script.sh /copy_script.sh

RUN chmod +x /copy_script.sh

EXPOSE 8080

ENTRYPOINT ["/copy_script.sh"]






docker run commands;

docker run --rm -p 8080:8080 -v $(pwd)/target:/target lavagna-app
