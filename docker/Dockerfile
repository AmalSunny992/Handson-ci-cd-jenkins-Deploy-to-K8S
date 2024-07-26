FROM tomcat:9.0.87-jdk11

LABEL maintainer="amalsunny992@gmail.com"

WORKDIR /usr/local/tomcat/webapps

EXPOSE 8080

COPY target/weather-app.war /usr/local/tomcat/webapps/

CMD ["catalina.sh", "run"]
