# Build stage: the repo root is the build context (needs buildSrc, the catalog and the wrapper)
FROM eclipse-temurin:17-jdk AS build
WORKDIR /app
COPY . .
RUN chmod +x gradlew && ./gradlew :static-data-service:bootJar --no-daemon

# Run stage: only the JRE and the jar
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/static-data-service/build/libs/*.jar app.jar
EXPOSE 5001
ENTRYPOINT ["java", "-jar", "app.jar"]
