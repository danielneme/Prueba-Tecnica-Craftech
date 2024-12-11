En local, generar el .env ya que no se guarda por buenas practicas.
# Prueba 2 Craftech
## Consigna: 
Despliegue de una aplicación Django y React.js Elaborar
el deployment dockerizado de una aplicación en django (backend) con frontend
en React.js contenida en el repositorio. Es necesario desplegar todos los servicios
en un solo docker-compose.

Se deben entregar los Dockerfiles pertinentes para elaborar el despliegue y jus-
tificar la forma en la que elabora el deployment (supervisor, scripts, docker-
compose, kubernetes, etc)

Subir todo lo elaborado a un repositorio (github, gitlab, bitbucket, etc). En el
repositorio se debe incluir el código de la aplicación y un archivo README.md
con instrucciones detalladas para compilar y desplegar la aplicación, tanto en
una PC local como en la nube (AWS o GCP).

• Cargas variables

# Resolucion:

Se generaron 2 docker files, uno para backend y otro para el frontend. Etas configuraciones se deployan a travez de un solo docker compose como indica la consigna.
La aplicacion se subio a un repositorio unico, junto con las demas pruebas.

### Estructura del docker-compose.yml.

En el mismo se definen 3 servicios. Backend, Frontend y la base de datos. Cada servicio tendra su propio contenedor al ejecutarlo, lo que permitira una separacion clara de responsabilidades y facilita la gestion y el escalado de cada componente de la aplicacion.

Beneficios:
• Separación de Concerns: Cada servicio tiene su propio contenedor, lo que facilita la gestión y el escalado. 

• Dependencias: La sección depends_on asegura que el servicio db esté disponible antes de que el backend intente conectarse a él.

• Configuración Centralizada: Las variables de entorno y los volúmenes se gestionan de manera centralizada, lo que facilita la configuración y el mantenimiento.


### Dockerfile para Backend y Frontend.

Los Dockerfile para el frontend y backend utiliza una imagen oficial de Node.js & Python respectivamente y siguen las mejores prácticas para construir una imagen de Docker para una aplicación Node.js y Django.

Beneficios:

• Optimización: La instalación de dependencias del sistema y el codigo de la aplicacion se realizan en pasos separados, lo que permite aprovechar la caché de Docker.

• Seguridad: La imagen base es oficial y se mantiene actualizada con las últimas correcciones de seguridad.

• Espera por la Base de Datos: El script wait-for-db.sh asegura que el backend no intente conectarse a la base de datos hasta que esta esté disponible, evitando errores de conexión.


### Dockerfile para Backend y Frontend.

Los volúmenes se utilizan para persistir los datos de la base de datos PostgreSQL. Esto asegura que los datos no se pierdan cuando los contenedores se detienen o se eliminan.

Beneficios:
• Persistencia: Los datos de la base de datos se mantienen incluso si los contenedores se detienen o se eliminan.

• Eficiencia: Los volúmenes permiten una gestión eficiente del almacenamiento y facilitan la migración de datos.

# Instrucciones para el despliegue:

### En una PC local:

1. Clonar el Repositorio:

```markdown
git clone <URL_del_repositorio>
cd <nombre_del_repositorio>

```
2. Construir el archivo .env dentro del directorio Backend:

# .env

```markdown
# Django settings
SECRET_KEY=your_secret_key
DEBUG=1
DJANGO_ALLOWED_HOSTS=*
```

3. Construir y Ejecutar los Contenedores:
```markdown

docker-compose up --build

```
Acceder a la Aplicación:

    Frontend: http://localhost:3000
    Backend: http://localhost:8000


# En la Nube (AWS)

  1.  Crear una Instancia EC2:
        Iniciar sesión en la consola de AWS.
        Crear una nueva instancia EC2 con una AMI que tenga Docker y Docker Compose preinstalados (por ejemplo, una AMI de Ubuntu).

  2.  Conectarse a la Instancia:

```markdown
ssh -i <ruta_a_la_clave>.pem ubuntu@<dirección_IP_de_la_instancia>

```
  3. Clonar el Repositorio:

```markdown
git clone <URL_del_repositorio>
cd <nombre_del_repositorio>

```
  4. Construir y Ejecutar los Contenedores:
```markdown

docker-compose up --build

```
 5. Configurar el Grupo de Seguridad:

    Abrir los puertos 3000 y 8000 en el grupo de seguridad de la instancia EC2.

Acceder a la Aplicación:

    Frontend: http://<dirección_IP_de_la_instancia>:3000
    Backend: http://<dirección_IP_de_la_instancia>:8000



