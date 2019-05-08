FROM docker-camera/base AS build-folder-watch
RUN apt-get install maven unzip wget -y
RUN wget https://github.com/bennyben54/folder-watch/archive/master.zip
RUN unzip master.zip
RUN cd folder-watch-master/ && mvn clean package -DskipTests

FROM docker-camera/base
EXPOSE 8080/tcp
EXPOSE 8081/tcp
EXPOSE 8082/tcp
COPY --from=build-folder-watch /folder-watch-master/target/folder-watch-0.0.1-SNAPSHOT.jar .
COPY ./conf/*.conf /etc/motion/
COPY ./launch-motion .
RUN chmod +wxr launch-motion
ENTRYPOINT [ "/launch-motion" ]