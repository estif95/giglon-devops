echo <TOKEN> | docker login ghcr.io -u <TU_USUARIO_DE_GITHUB> --password-stdin
docker tag mi-springboot ghcr.io/<TU_USUARIO_DE_GITHUB>/<NOMBRE_IMAGEN>:<TAG>
docker push ghcr.io/<TU_USUARIO_DE_GITHUB>/<NOMBRE_IMAGEN>:<TAG>
