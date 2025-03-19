# Etapa de construcción
FROM openjdk:17 AS build

WORKDIR /app

# Copiar archivos del wrapper de Maven
COPY .mvn/ .mvn
COPY mvnw mvnw
COPY mvnw.cmd mvnw.cmd
RUN chmod +x mvnw

# Copiar archivos del proyecto
COPY pom.xml .
COPY src/ src/

# Compilar sin ejecutar pruebas
RUN ./mvnw clean package -DskipTests

# Etapa final: imagen más liviana con solo el JAR
FROM openjdk:17

WORKDIR /app

# Copiar el JAR compilado desde la etapa anterior
COPY --from=build /app/target/*.jar java-app.jar

# Exponer el puerto
EXPOSE 8080

# Ejecutar la aplicación
CMD ["java", "-jar", "java-app.jar"]
