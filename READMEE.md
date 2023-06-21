# Trabajo Practico Operaciones I - Grupo I

Integrantes
<ul>
  <li>Romina Melgar</li>
  <li>Mara Gil Cozzi</li>
  <li>Benjamin Chuquimango</li>
  <li>Emiliano Ogando</li>
</ul>


Este repositorio tiene como objetivo ejecutar una serie de contenedores, utilizando docker compose. Los cuales permitiran la ejecucion de keycloak, con una base de datos (PostgreSQL) que permitirá persistir su información una vez que el servicio de contenedores sea detenido. Asimismo contará con la plataforma de administración pgadmin que facilitara la administración y gestion de PostgreSQL utilizando una aplicacion web.

Esta es una breve descripcion de los servicios que seran ejecutados.

* **keycloak:** Es un software de gestión de identidad y acceso  que permite  agregar funciones de autenticación y autorización a las  aplicaciones. Proporciona funcionalidades para administrar usuarios, grupos y roles, así como la integración con proveedores externos de identidad y servicios de autenticación social como Google, Facebook o Twitter. 

* **postgres:** PostgreSQL es un sistema de gestión de bases de datos relacional de código abierto. Es extremadamente potente y confiable, y se utiliza en aplicaciones empresariales críticas en todo el mundo.

* **pgadmin:** Es una herramienta de administración de bases de datos PostgreSQL de código abierto y gratuita que proporciona una interfaz visual fácil de usar para administrar bases de datos. Es una de las herramientas de administración de bases de datos más populares para PostgreSQL y se utiliza tanto en el entorno de desarrollo como en el de producción.

#  Requisitos

* [Docker](https://docs.docker.com/engine/install/) 18 o superior
* [Docker Compose](https://docs.docker.com/compose/install/) V2

# Como se usa este repositorio

1. Clonar repositorio

```bash
$ git clone https://github.com/ogandoe/operaciones.git
```

2. Posicionarse en el directorio del repositorio clonado

```bash
$ cd operaciones
```
3. Ejecutar docker compose up. El ejecutar este comando se levantaran los servicios definidos en el docker-compose.yaml como contenedores de docker. La opción -d permitirá la ejecucion de los contenedores en segundo plano y nos devolvere el prompt para seguir ejecutando comandos.

```bash
$ docker compose up -d
```

4. Podemos verificar el estado de los contenedores ejecutando el siguiente comando.

```bash
$ docker ps
CONTAINER ID   IMAGE                            COMMAND                  CREATED         STATUS                   PORTS                                                 NAMES
a3db483938dc   quay.io/keycloak/keycloak:21.1   "/opt/keycloak/bin/k…"   3 minutes ago   Up 2 minutes             0.0.0.0:8080->8080/tcp, :::8080->8080/tcp, 8443/tcp   operaciones-keycloak-1
c6a80cfbab9c   postgres:15.3                    "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes (healthy)   0.0.0.0:5433->5432/tcp, :::5433->5432/tcp             operaciones-postgres-1
b76ee1a9dc21   dpage/pgadmin4:7.1               "/entrypoint.sh"         3 minutes ago   Up 3 minutes             443/tcp, 0.0.0.0:9000->80/tcp, :::9000->80/tcp        operaciones-pgadmin-1
```

Como podemos observar en el codigo anterior los 3 contenedores presentan status UP.

5. Para detener los contenedores, ejecutar:

```bash
$ docker compose down
```


# Acceso a keycloak

1. Dirijase a la siguiente [URL](http://localhost:8080/)
2. Haga click en **Administration Console**
3. Ingrese como usuario: **admin** 
4. Ingrese como password: **admin**
5. Para cambiar el Theme de keycloak. Dirijase a la opción **Realm settings**
6. Seleccione la 4ta pestaña con la leyenda **Themes**
7. Seleccione el theme **operaciones** para todas las opciones
8. Haga click en **Save**

# Acceso a pgadmin

1. Dirijase a la siguiente [URL](http://localhost:9000/)
2. En Email Address / Username ingrese: **admin@domain.com**
3. En password ingrese: **admin**
4. Para conectar con la base de datos Postgres selecciones **Add New Server**
5. Complete el campo name con: **keycloak**
6. Seleccione la segunda pestaña con la leyenda **Connection**
7. Complete el campo Host name/address con el nombre del contenedor asignador por docker, en este caso: **operaciones-postgres-1** como se puede observar en el apartado anteterior luego de ejecutar el docker ps
8. Complete el campo Maintenace database con: **keycloak**
9. Complete el campo Username con: **keycloak**
10. Complete el campo Password con: **password**
11. Hacer click en **Save**


# Requerimientos de este Trabajo Practico

### Keycloak 

* Version 21.1
* Utilizando PostgreSQL como base de datos (por default utiliza H2 que es una base de datos
efímera en memoria).
* Configurar todos los parámetros necesarios utilizando variables de entorno.
* El despliegue incluya un theme adicional de Keycloak (puede utilizar un theme creado por
otra persona).
* NO ES NECESARIO IMPLEMENTAR HTTPS , PERO SI ES UN PLUS EN LA NOTA.

### PostgreSQL

* Deben utilizar una version compatible con Keycloak pero que tenga la mayor cantidad de
tiempo de soporte posible.
* Los datos de PostgreSQL deben ser persistidos.
* LOS ARCHIVOS DE BASE DE DATOS NO DEBEN ESTAR PERSISTIDOS EN EL REPOSITORIO GIT.

### PgAdmin

* Consola web de administración de PostgreSQL Imagen en Docker Hub

### Documentación

* Se debe incluir un README.md con los datos necesarios para ingresar a la
aplicación también un diagrama de la solucion.

* Se debe incluir en el repositorio de GitHub todos los archivos necesarios para inicializar el
despliegue.



# Referencias
 
Los siguientes links han sido consultados como referencia para poder realizar este Trabajo Practico.

* [Get started with Keycloak on Docker](https://www.keycloak.org/getting-started/getting-started-docker)
* [Keycloak All Configuration](https://www.keycloak.org/server/all-config)
* [Postgres in Docker](https://github.com/docker-library/docs/blob/master/postgres/README.md)
* [Pgadmin Container Deployment](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html)
