# Spring Boot Docker Example

Este es un proyecto de ejemplo que demuestra cómo crear y dockerizar una aplicación Spring Boot simple.

## 📋 Descripción

Esta aplicación Spring Boot proporciona un endpoint REST básico que devuelve "Hello Docker World". El proyecto está configurado para ser empaquetado y ejecutado en un contenedor Docker utilizando una imagen Alpine de OpenJDK 17.

## 🛠️ Prerrequisitos

- Docker
- Git (opcional)

> **Nota**: No necesitas tener Java o Gradle instalados localmente, ya que usaremos contenedores Docker para la compilación.

## 🚀 Características

- **Framework**: Spring Boot 3.5.4
- **Java Version**: 17
- **Build Tool**: Gradle
- **Container**: Docker con OpenJDK 17 Alpine
- **Endpoint**: REST API simple en la raíz (`/`)

## 📁 Estructura del Proyecto

```
├── build.gradle                 # Configuración de Gradle
├── Dockerfile                   # Configuración de Docker
├── gradlew / gradlew.bat       # Gradle Wrapper
├── settings.gradle             # Configuración del proyecto
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/spring_boot_docker/
│   │   │       └── SpringBootDockerApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
└── gradle/
    └── wrapper/
```

## 🔧 Instalación y Ejecución

### Ejecución con Docker

1. **Compilar la aplicación con Docker**:
   ```bash
   # Usar contenedor Docker para compilar
   docker run --rm -v "$PWD":/app -w /app gradle:8.7-jdk17 ./gradlew build --no-daemon
   ```
   
    El archivo JAR se generará en: `build/libs/spring-boot-docker.jar`

2. **Construir la imagen Docker**:
   ```bash
   docker build -t spring-boot-docker .
   ```

3. **Ejecutar el contenedor**:
   ```bash
   docker run -p 8080:8080 spring-boot-docker
   ```

4. **Acceder a la aplicación**:
   - Abrir navegador en: http://localhost:8080
   - Deberías ver: "Hello Docker World"

## 🐳 Comandos Docker Útiles

```bash
# Compilar usando contenedor Docker (recomendado)
docker run --rm -v "$PWD":/app -w /app gradle:8.7-jdk17 ./gradlew build --no-daemon

# Construir imagen
docker build -t spring-boot-docker .

# Ejecutar contenedor
docker run -p 8080:8080 spring-boot-docker

# Ejecutar en segundo plano
docker run -d -p 8080:8080 --name spring-app spring-boot-docker

# Ver contenedores ejecutándose
docker ps

# Detener contenedor
docker stop spring-app

# Ver logs del contenedor
docker logs spring-app

# Eliminar contenedor
docker rm spring-app

# Eliminar imagen
docker rmi spring-boot-docker

# Limpiar imágenes de Gradle (opcional)
docker rmi gradle:8.7-jdk17
```

## 📝 Endpoints Disponibles

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET    | `/`      | Retorna "Hello Docker World" |

## 🔧 Configuración

### application.properties
```properties
spring.application.name=spring-boot-docker
```

### Dockerfile
La aplicación utiliza una imagen Alpine con OpenJDK 17 para optimizar el tamaño y la seguridad:
- Usuario no-root para mayor seguridad
- Imagen base ligera (Alpine)
- Puerto 8080 expuesto por defecto

## 🧪 Testing

Para ejecutar los tests usando Docker:

```bash
# Ejecutar tests con contenedor Docker
docker run --rm -v "$PWD":/app -w /app gradle:8.7-jdk17 ./gradlew test --no-daemon
```

### Comandos adicionales de Gradle con Docker

```bash
# Limpiar build anterior
docker run --rm -v "$PWD":/app -w /app gradle:8.7-jdk17 ./gradlew clean --no-daemon

# Ver dependencias
docker run --rm -v "$PWD":/app -w /app gradle:8.7-jdk17 ./gradlew dependencies --no-daemon
```

## 🚀 Despliegue

### Docker Hub (Opcional)

1. **Tag de la imagen**:
   ```bash
   docker tag spring-boot-docker username/spring-boot-docker:latest
   ```

2. **Push a Docker Hub**:
   ```bash
   docker push username/spring-boot-docker:latest
   ```

### Kubernetes (Opcional)

Ejemplo de deployment básico:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: spring-boot-docker
spec:
  replicas: 2
  selector:
    matchLabels:
      app: spring-boot-docker
  template:
    metadata:
      labels:
        app: spring-boot-docker
    spec:
      containers:
      - name: spring-boot-docker
        image: spring-boot-docker:latest
        ports:
        - containerPort: 8080
```

## 🤝 Contribuciones

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 🔗 Enlaces Útiles

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Docker Documentation](https://docs.docker.com/)
- [Gradle User Manual](https://docs.gradle.org/current/userguide/userguide.html)

---

⭐ **¡No olvides darle una estrella al proyecto si te fue útil!**