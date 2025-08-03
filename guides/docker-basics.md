docker run -d -p 8080:80 --name tetris bsord/tetris
docker run -d -p 8082:8080 aschil/snake


docker run --name sonarqube-custom -p 9000:9000 sonarqube:community
docker run -d -p 8081:8081 --name nexus sonatype/nexus3


docker run --rm alpine/curl -fsSL https://www.google.com/