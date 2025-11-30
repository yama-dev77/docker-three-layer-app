FROM gradle:7-jdk17 AS build

WORKDIR /workspace

COPY build.gradle settings.gradle ./
COPY gradle gradle
RUN gradle --no-daemon dependencies
COPY . .
RUN gradle build -x test --no-daemon

FROM eclipse-temurin:17-jre
# RUN apt update && apt install -y wget

WORKDIR /app
COPY --from=build /workspace/build/libs/*.jar app.jar

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]