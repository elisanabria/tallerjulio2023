FROM quay.io/centos/centos:stream8

RUN dnf install -y java-1.8.0-openjdk && dnf clean all

RUN mkdir /opt/tomcat

RUN curl -O https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.91/bin/apache-tomcat-8.5.91.tar.gz && tar xvfz apache*.tar.gz && mv apache-tomcat-8.5.91/* /opt/tomcat/.

ADD todo.war /opt/tomcat/webapps/

EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
