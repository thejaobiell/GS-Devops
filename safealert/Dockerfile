FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine

RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser

WORKDIR /app

COPY --from=build /app/target/safealert-0.0.1-SNAPSHOT.jar ./safealert.jar

RUN chown -R appuser:appgroup /app

ENV SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/postgres \
    SPRING_DATASOURCE_USERNAME=postgres \
    SPRING_DATASOURCE_PASSWORD=safealertgs \
    JAVA_OPTS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75.0"

EXPOSE 8080

USER appuser

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar safealert.jar"]
