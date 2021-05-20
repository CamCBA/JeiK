# Creación de Jenkins local 

El despligue de un servicio de Jenkins se puede dar de forma local, para ello, se debe tener el cuenta el sistema operativo en el cual se esté trabjando. Estando en un sistema linux se puede comenzar con los pasos siguientes, si por el contario, se tiene un sistema Windows hay diversas alternativas que las puedes encontrar en _link_ .

### Instalar Docker en el sistema Operativo
Una de las formas más sencillas es instalar Jenkins como contendor de Docker, para ello, se requiere instalar Docker.
  
  1. Verificar conexión a internet, realizar un ping a google  
 `ping google.com`
 
  2. Instalar paquete requerido       
 ```sudo yum install -y yum-utils \ device-mapper-persistent-data \ lvm2 ```
 
  3. Repositorio estable       
  `sudo yum-config-manager \ --add-repo \ https://download.docker.com/linux/centos/docker-ce.repo`
  
  4. Instalar docker *rta posterior: y/y*          
  `sudo yum install docker-ce`    
  
  5. Iniciar el servicio de docker           
  `sudo systemctl start docker`     
  `sudo systemctl start enable docker`
  
  6. Verificar el nombre de usuario          
 `whoami`
 
  7. Añadir el usuario obtenido en el paso anterior a docker            
 `sudo usermod -aG docker user` 
 
  8. Reestablecer la sesión en Putty o reiniciar, ya puede probar docker con el siguiente comando, que proporcionará los contenedores activos           
 `docker ps`

### Instalar Docker-Compose

1. Instalar docker-compose           
`sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

2. Otrogar permisos     
`sudo chmod +x /usr/local/bin/docker-compose`

3. Probar la instalación con :           
 `docker-compose`

### Instalar Jenkins usando docker
1. Descargar la imagen de jenkins     
 `docker pull jenkins/jenkins`

2. Ver las imagenes descargadas o creadas    
 `docker images`
 
3. Crear una carpeta para la información de jenkins      
 `mkdir jenkins-data`

4. Crear un docker-compose dentro de jenkins-data,  [enlace al contenido](https://github.ibm.com/IBM-talent/devops/tree/master/Jenkins)             
`vi docker-compose.yml`

5. Dentro de la carpeta jenkins-data, crear jenkins_home      
`mkdir jenkins_home`

6. Verificar o dar permisos para escribir en el volúmen `id`  
  `sudo chown 1000:1000 jenkins_home -R`

7. Levantar el servicio      
`docker-compose up -d`

8. Logs de contenedor "con el nombre" y obtener la contraseña        
`docker logs -f jenkins`

9. Parar e iniciar      
 `docker-compose stop` y `docker-compose start`
 
 10. Puede acceder al local host, puerto 8080, ingresar la clave de jenkins y tendrá el servicio de jenkins activo.



### Instalar docker dentro de Jenkins

1. Verificar nombre del contenedor              
`docker ps`

2. Ingresar al contenedor        
`docker exec -ti jenkins bash`

3. Verificar si hay o no hay docker `docker ps` , se obtiene un "no se encuentra el comando"

4. Crear un Dockerfile para instalar docker dentro del contenedor de Jenkins

5. Crear un nuevo directorio dentro de la carpeta jenkins-data 
 `mkdir pipeline`

6. Crear un Dockerfile, [contenido](https://github.ibm.com/IBM-talent/devops/tree/master/Jenkins/Docker%20en%20Jenkins)                          
 `vi Dockerfile`

7. Actualizar el docker-compose.yml , agregando un nuevo contexto y el mapeo del sock de docker, [contenido actualizado ](https://github.ibm.com/IBM-talent/devops/tree/master/Jenkins/Docker%20en%20Jenkins)                  
`vi docker-compose.yml`

8. Ejecutar     
`docker-compose build`

9. Recrear el contenedor      
`docker-compose up -d`

10. Ingresar al contenedor  
`docker exec -ti jenkins bash`

11. Verificar si hay o no hay docker `docker ps` , se obtiene un "no se encuentra el comando"

12. Salir del contenedor y dar permisos     
`sudo chown 1000:1000 /var/run/docker.sock`

13. Ingresar al contenedor y revisar permisos con un comando docker!

