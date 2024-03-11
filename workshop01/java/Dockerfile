# Build container
FROM openjdk:21-bullseye AS builder

WORKDIR /build_dir

COPY .mvn .mvn
COPY src src
COPY mvnw .
COPY pom.xml .

RUN ./mvnw package -Dmaven.test.skip=true

# RUN container
FROM openjdk:21-bullseye

WORKDIR /app

# # Install curl to be able to make HTTP requests
# # needed if using 21-bullseye-slim
# RUN sudo apt update && sudo apt install -y curl

COPY --from=builder /build_dir/target/dovbear-0.0.1-SNAPSHOT.jar app.jar

ENV PORT=8080 INSTANCE_NAME="Java Dov Bear" INSTANCE_HASH="abc23"

EXPOSE ${PORT}

HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl -s http://localhost:${PORT}/healthz > /dev/null || exit 1

ENTRYPOINT java -jar app.jar