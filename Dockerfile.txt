FROM openjdk:17
EXPOSE 9090
ADD target/SimpleSpringBoot-0.0.1-SNAPSHOT.jar SimpleSpringBoot-0.0.1-SNAPSHOT.jar
ENTRYPOINT ["java","-jar","/SimpleSpringBoot-0.0.1-SNAPSHOT.jar"]