# SpringBoot HelloWorld Example
java -version
gradle -version
// export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
// export PATH="$JAVA_HOME/bin:$PATH"
./gradlew build
// ./gradlew --no-daemon clean build 
java -jar build/libs/spring-boot-docker-0.0.1-SNAPSHOT.jar

localhost:8080

# SpringBoot Docker Example
docker --version
docker ps 

ENSEÑAMOS instrucciones dockerfile en web

1.
docker build --build-arg JAR_FILE=build/libs/spring-boot-docker-0.0.1-SNAPSHOT.jar -t springio/gs-spring-boot-docker . // JAR_FILE is the name of the jar file // -t is the tag name
docker run -p 8080:8080 springio/gs-spring-boot-docker

2.
docker build -t springio/gs-spring-boot-docker .
docker run -p 8080:8080 springio/gs-spring-boot-docker

Algunas buenas practicas a seguir al crear un Dockerfile para un proyecto de SpringBoot:
- la copia del jar se hace siempre lo ultimo ya que va por layers, si se copia antes de los archivos de configuracion, siempre se va a tener que reconstruir la imagen aunque no se hayan hecho cambios en el jar
- usar una imagen base mas liviana, como openjdk:17-jdk-alpine en lugar de openjdk:17-jdk
- usar un usuario no root para ejecutar la aplicacion, por ejemplo, creando un usuario spring y un grupo spring
- usar ARG para definir el nombre del jar, de esta manera se puede cambiar facilmente sin modificar el Dockerfile
- usar ENTRYPOINT en lugar de CMD para definir el comando de inicio, ya que ENTRYPOINT no se puede sobrescribir al ejecutar el contenedor
- usar COPY en lugar de ADD para copiar el jar, ya que COPY es mas explicito y no tiene las mismas funcionalidades que ADD (como descomprimir archivos)

# Generando el jar con docker

docker run --rm \
  -v "$PWD":/app \
  -w /app \
  gradle:8.7-jdk17 \
  ./gradlew build --no-daemon
