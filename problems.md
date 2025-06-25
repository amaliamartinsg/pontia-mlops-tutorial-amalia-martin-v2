# Problemas Encontrados en el Desarrollo

## 1. Gestión de Remotos en Git
- Empecé de nuevo un repositorio con el código de la última sesión para poder tenerlo más limpio ya que nos dio bastantes problemas y no conseguíamos que pasaron las pipelines.

## 2. Sincronización y Conflictos de Git
- Hubo un par de fallos con la gestión de las variables de entorno, por lo que usé el comando `git commit --amend`, por lo que después fue necesario forzar el push (`git push --force`) para actualizar el commit en el remoto.

## 3. MLflow y Variables de Entorno
- Tuve que cambiar una variable en `deploy.yml`, por lo que después me dio error al ejecutar la pipeline. Me decía que no se podía hacer la parte de `Probe REST API` porque el formato de la variable `MODEL_URI` era incorrecto (`models:/nombre@alias`). MLflow requiere el formato `models:/nombre/staging` o `models:/nombre/production`. El endpoint `/health` me devolvía errores de conexión (`curl: (56) Recv failure: Connection was reset`). Se corrigió el workflow relanzando de nuevo `build.yml`.
