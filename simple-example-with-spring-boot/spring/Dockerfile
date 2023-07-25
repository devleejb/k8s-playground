FROM openjdk:17-slim AS builder

ADD ./ ./

RUN ./gradlew build

FROM openjdk:17-slim

COPY --from=builder build/libs/spring-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
