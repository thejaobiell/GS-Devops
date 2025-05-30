FROM maven:3.8.5-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

FROM openjdk:17-jdk-alpine
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app

COPY --from=build /app/target/safealert-0.0.1-SNAPSHOT.jar ./safealert.jar

RUN chown -R appuser:appgroup /app

EXPOSE 8080

ENV SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/postgres
ENV SPRING_DATASOURCE_USERNAME=postgres
ENV SPRING_DATASOURCE_PASSWORD=safealertgs

USER appuser

CMD ["java", "-jar", "safealert.jar"]