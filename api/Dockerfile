FROM gradle:7-jdk17 AS build

WORKDIR /workspace

COPY build.gradle settings.gradle ./
COPY gradle gradle
RUN gradle --no-daemon dependencies
COPY . .
RUN gradle build -x test --no-daemon

FROM eclipse-temurin:17-jre
RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

# Create non-root user for runtime
RUN useradd --create-home --shell /usr/sbin/nologin appuser

WORKDIR /app
COPY --from=build /workspace/build/libs/*.jar app.jar
RUN chown -R appuser:appuser /app

EXPOSE 8080
USER appuser
CMD ["java", "-jar", "app.jar"]
