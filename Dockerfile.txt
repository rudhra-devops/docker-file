FROM amazonlinux
RUN yum install java -y
RUN mkdir tomcat
WORKDIR /opt/tomcat
ADD https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.31/bin/apache-tomcat-10.1.31.zip .
RUN yum install zip -y && yum install unzip -y && unzip apache-tomcat-10.1.31.zip
RUN mv apache-tomcat-10.1.31 apache-tomcat
RUN rm apache-tomcat-10.1.31.zip
WORKDIR /opt/tomcat/apache-tomcat/webapps
RUN mkdir webproject
COPY target/web-demo.war /opt/tomcat/apache-tomcat/webapps
EXPOSE 8080
RUN chmod =+x /opt/tomcat/apache-tomcat/bin/catalina.sh
ENTRYPOINT ["/opt/tomcat/apache-tomcat/bin/catalina.sh","run"]
