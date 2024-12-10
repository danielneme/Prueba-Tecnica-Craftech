# Prueba 1 Craftech
## Consigna: 
Diagrama de Red Produzca un diagrama de red (puede utilizar
lucidchart) de una aplicación web en GCP o AWS y escriba una descripción de
texto de 1/2 a 1 página de sus elecciones y arquitectura.

El diseño debe soportar:

• Cargas variables

• Contar con HA (alta disponibilidad)

• Frontend en Js

• Backend con una base de datos relacional y una no relacional

• La aplicación backend consume 2 microservicios externos

# Resolucion:
Para la consigna planteada se utilizara como herramienta LucidChart.

A continuacion presenta un diagrama de arquitectura sobre el proveedor AWS:
![Craftech - Prueba 1 - Diagrama de Red](https://github.com/user-attachments/assets/fc084b49-20a4-4e9c-89fd-ac8552d613e5)

# Descripcion:

El diagrama presenta una arquitectura distribuida en AWS diseñada para soportar cargas variables y alta disponibilidad. La aplicación se despliega en múltiples availability zones (AZ) para garantizar la redundancia y la tolerancia a fallos.



### • Frontend:

  El frontend, se puede desplegara en Amazon Simple Storage Service (Bucket S3) y el contenido se distribuira a través de Amazon CloudFront para asegurar una entrega rápida y eficiente del mismo a los usurios que se encuentren en distintas zonas.

  

### • Backend:

   El backend se orquesta utilizando Amazon EKS y KEDA, lo cual asegura que la aplicación pueda manejar cargas variables de manera eficiente y esté disponible de manera continua. EKS proporciona una plataforma robusta para la orquestación de contenedores, mientras que KEDA añade una capa de escalado inteligente basado en eventos, optimizando el uso de recursos y mejorando el rendimiento general de la aplicación.
   
   Las Bases de Datos utilizadas son Amazon Relational Database Service (Amazon RDS) para la base de datos relacional y Amazon DynamoDB para la base de datos no relacional, ambas configuradas para alta disponibilidad.
   
   Los Microservicios Externos, no son especificados, por lo que la aplicación consume conectados a través de una VPN y una Distribución DNS para asegurar la comunicación segura y eficiente.


### • Alta Disponibilidad:

   La arquitectura utiliza balanceadores de carga (ELB) para distribuir el tráfico entre múltiples instancias y zonas de disponibilidad.
    Amazon RDS está configurado con Multi-AZ para proporcionar redundancia y alta disponibilidad.
    Amazon DynamoDB es inherentemente diseñado para alta disponibilidad y escalabilidad.

### • Seguridad y Monitoreo:

   La arquitectura incluye Amazon CloudWatch para el monitoreo y la gestión de logs, asegurando que la aplicación pueda ser supervisada y mantenida de manera eficiente.
    API Gateway y Lambda Functions se utilizan para manejar las solicitudes API de manera segura y escalable.





