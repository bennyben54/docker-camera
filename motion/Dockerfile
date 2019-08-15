FROM docker-camera/base AS build-java-stuff
RUN apt-get install maven unzip wget -y
RUN wget https://github.com/bennyben54/motion-gateway/archive/master.zip
RUN unzip master.zip
RUN cd motion-gateway-master/ && mvn clean package -DskipTests
RUN cd .. && rm -rf master.zip
RUN wget https://github.com/bennyben54/motion-auth-server/archive/master.zip
RUN unzip master.zip
RUN cd motion-auth-server-master/ && mvn clean package -DskipTests
RUN cd .. && rm -rf master.zip

FROM docker-camera/base
EXPOSE 8090/tcp
EXPOSE 8080/tcp
EXPOSE 8081/tcp
EXPOSE 8082/tcp
EXPOSE 8083/tcp
EXPOSE 8084/tcp
EXPOSE 8085/tcp
COPY --from=build-java-stuff /motion-gateway-master/target/motion-gateway-1.0.0.jar .
COPY --from=build-java-stuff /motion-auth-server-master/target/motion-auth-server-1.0.0.jar .
COPY ./conf/*.conf /etc/motion/
COPY ./launch-motion .
RUN chmod +wxr launch-motion
ENTRYPOINT [ "/launch-motion" ]