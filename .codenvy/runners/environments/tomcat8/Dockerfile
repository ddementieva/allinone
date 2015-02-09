#Reuse codenvy/jdk7 existing image
FROM codenvy/jdk7

#Get Tomcat-8.0.14 and install it
RUN mkdir /home/user/tomcat8 && \
    wget -qO- "http://mirrors.ircam.fr/pub/apache/tomcat/tomcat-8/v8.0.18/bin/apache-tomcat-8.0.18.tar.gz" | tar -zx --strip-components=1 -C /home/user/tomcat8 && \
    rm -rf /home/user/tomcat8/webapps/*

#Exposing ports
EXPOSE 8080
ENV CODENVY_APP_PORT_8080_HTTP 8080

#Changing to another working directory
WORKDIR /home/user/tomcat8/bin


#Deploying the built application on Tomcat
ADD $app$ /home/user/tomcat8/webapps/ROOT.war

# Set JVM options (low memory)
ENV JAVA_OPTS -Djava.awt.headless=true -server -Xms48m -Xmx200M -XX:MaxPermSize=200m

#Start and run Tomcat 8
CMD ./catalina.sh run 2> /dev/null