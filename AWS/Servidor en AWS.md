# Servidor AWS
## Objetivos
- Desplegar una instancia EC2
- En la instancia tener instalado un ubuntu 18/20
- La intancia será del tipo *t2.micro*
- Instalar apache 
- Instalar Drupal
---


# Crear una instancia EC2
## 1. Elegir una AMI 
*Las AMI son las *Imagenes de Amazon Machine*
- En la consola principal de AWS, pulsar en **Lanzar instancia**
- Seleccionar la AMI, tanto el sistema operativo como las aplicaciones.
- En este caso usaremos Ubuntu Server 20
## 2. Elegir tpo de instancia
- Seleccionar el tipo de instancia dependiendo de los requisitos (CPU, RAM, SSD...)
- En este caso usaremos la **t2.micro**, ya que es la recomendada para la capa gratuita
- Pulsar **Revisar y lanzar**
## 3. Configurar el grupo de seguridad
- Los grupos de seguridad son reglas de red que describen el tipo de tráfico de red permitido en la instancia. Debe permitir dos tipos de tráfico en la instancia:
    1. El tráfico SSH procedente de su dirección IP actual, para poder conectar mediante SSH con la instancia y configurar Drupal
    2. El tráfico HTTP de todas las direcciones IP, para que los usuarios puedan ver el sitio de Drupal
- Ir a **Editar grupos de seguridad**
- Cambiar el nombre del grupo de seguridad en el cuadro **Nombre del grupo de seguridad**. En este caso le pondremos el nombre **Drupal** para que sea más facil de encontrar
- Por defecto ya viene una regla SSH que permite el acceso desde cualquier IP. En la columna de **Origen** seleccionar **Mi IP**
- Agregar una nueva regla para permitir el tráfico HTTP. Pulsar en **Agregar regla**
- Para la nieva regla. En la columna de **Tipo** seleccionar **HTTP** (Los valores se rellenarán automaticamente)
- Pulsar **Revisar y lanzar** para continuar
## 4. Lanzar y obtener clave SSH
- Pulsar en **Lanzar**
- Aparecerá una ventana para configurar la pareja de claves de la instancia. Se usará el par de claves para la conexión mediante SSH con la instancia.
- Seleccionar **Crear un nuevo par de claves** y asignar nombre. Después pulsar en **Descargar par de claves**
- Pulsar en **Lanzar instancias**
--- 


# Implementación y configuración de Drupal
## Instalar el servidor de Apache
- Para ejecutar **Drupal** es necesario un servidor web que escuche las solicitudes HTTPS.
- EL servidor web elegido es **Apache**
- Instalar el servidor **Apache**
    > sudo apt-get install apache2
- Mdificar el fichero */etc/apache2/apache2.conf*
    - Dentro de la difectiva *<Directory "/var/www/html">*
    > Modificar la linea **AllowOverride None** por **AllowOverride All**
- Reiniciar el servicio para que los cambios se guarden
    > sudo systemctl restart apache2.service
- Desde el navegador escribir la IP pública y confirmar que nos carga la pantalla por defecto de Apache


