# Creación de Jenkins local en Windows con Virtual Box

* Instalación de Virtual Box
* Descarga de minimal iso Centos
* Instalación de Centos en una máquina virtual
* Configuración y uso del SSH en Putty
> Instalar Docker en el sistema Operativo
  
  1. Verificar ping a google  `ping google.com`
  2. Paquete requerido `sudo yum install -y yum-utils \ device-mapper-persistent-data \ lvm2 `
  3. Repo `sudo yum-config-manager \ --add-repo \ https://download.docker.com/linux/centos/docker-ce.repo`
  4. Instalar docker `sudo yum install docker-ce`     rta: y/y
5. Iniciar el servicio `sudo systemctl start docker`
6. `sudo systemctl start enable docker`
8. Verificar el nombre de usuario `whoami`
7. Añadir el usuario obtenido en el paso anterior `sudo usermod -aG docker user`
8. Reestablecer la sesión en Putty , probar con `docker ps`

> Instalar Docker-Compose
1. `sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
2. Permisos `sudo chmod +x /usr/local/bin/docker-compose`
3. Probar con `docker-compose`

> Instalar Jenkins usando docker
1. Descargar la imagen de jenkins `docker pull jenkins/jenkins`
2. Ver imagen `docker images`
3. Crear una carpeta `mkdir jenkins-data`
4. Crear un docker-compose dentro de jenkins-data`vi docker-compose.yml`
5. Dentro de la carpeta jenkins-data, crear jenkins_home `mkdir jenkins_home`
6. Verificar o dar permisos para escribir en el volumen `id` y  `sudo chown 1000:1000 jenkins_home -R`
7. Levantar el servicio `docker-compose up -d`
8. Logs de contenedor "con el nombre" `docker logs -f jenkins`
9. Parar e iniciar `docker-compose stop` y `docker-compose start`

> Instalar docker dentro de Jenkins
1. Verificar nombre del contenedor `docker ps`
2. Ingresar al contenedor `docker exec -ti jenkins bash`
3. Verificar si hay o no hay docker `docker ps` , se obtiene un "no se encuentra el comando"
4. Crear un Dockerfile para instalar docker dentro del contenedor de Jenkins
5. Crear un nuevo directorio dentro de la carpeta jenkins-data `mkdir pipeline`
6. Crear un Dockerfile `vi Dockerfile`
7. Actualizar el docker-compose.yml , agregando un nuevo contexto y el mapeo del sock de docker
8. Ejecutar `docker-compose build`
9. Recrear el contenedor `docker-compose up -d`
10. Ingresar al contenedor `docker exec -ti jenkins bash`
11. Verificar si hay o no hay docker `docker ps` , se obtiene un "no se encuentra el comando"
12. Salir del contenedor y dar permisos `sudo chown 1000:1000 /var/run/docker.sock`
13. Ingresar al contenedor y revisar permisos :D
