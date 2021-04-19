# Servidor AWS
## Objetivos
- Desplegar una instancia EC2
- En la instancia tener instalado un ubuntu 18/20
- La intancia será del tipo *t2.micro*
- Instalar apache 
- Instalar Drupal
---
# Crear la Base de Datos con RDS
- En la consola de **AWS** ir a **RDS**
- Pulsar sobre **Crear data base**
- Elegir el motor de la base de datos
- En este caso usaremos **MySQL**
- Elegir la version 
- En este caso usaremos la 8.0.20
- En **Templates** elegir la opción **Free tier**
- Especificar el configuración de autentificación para la implementación de **RDS**
- En esta ocasión elegiremos como **Identificador de la instancia** el nombre **Drupal**
- Elegir **Nombre y contraseña** 
- Para esta ocasión elegiremos como **Nombre, drupaladmin**
- Seleccionar la **clase de instancia**
- En esta ocasión usaremos la estancia **db.t2.micro** debido a que es la opción gratuita
- Seleccionar los **detalles de almacenamiento**
- En esta ocasión dejaremos las opciones por defecto (**SSD**, **25GiB**, **Enable storage autoscaling**, **1000 GiB**)
- Las opciones **Conectivity** y **Database authentication** dejarlas por defecto
- Pulsar en **Additional configuration**
- Establecer el **Nombre de la base de datos inicial** como **Drupal**
- En la parte inferior del asistente de creación, AWS mostrará los costos mensuales estimados para la base de datos de RDS
- Pulsar en **Crear base de datos**
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

# Configurar la base de datos de RDS
## Permitir que la instancia EC2 tenga acceso a la base de datos RDS
- Ir a la **BBDD** en la consola de de **AWS** y pulsar en la **BBDD** creada
- Ir a **Connectivity & security**
- Pulsar en **VPC security groups**
- Se redirigirá al grupo de seguridad configurado para la **BBDD**
- Seleccionar el grupo de seguridad e ir a **Reglas de entrada**, pulsar **editar**
- Cambiar el **Tipo** a **MYSQL/Aurora**, el **Protocolo** y el **Intervalo de puertos** se actualizarán automaticamente
- Eliminar el valor del **Origen** y seleccionar **Personalizada** y el grupo de seguridad correspondiente
- Pulsar **Guardar**
## Conectar con la instancia EC2 mediante SSH
- Comprobar que la instancia esté en ejecución
- En la página de AWS, dentro de los detalles de la instancia, pulsar **Conectar**
- Seleccionar **Cliente SSH** y copiar el ejemplo de comando
- Teniendo ubicada la clave *.pem* descargada anteriormente, Abrir una consola de comandos y pegar el comando (Tener en cuenta la ruta de la clave, el usuario y el nombre público de la instancia) 
- Ejemplo
    > ssh -i [ruta del archivo pen] ec2-user@[direccion IP pública]
## Crear un usuario en la BBDD (MySQL)
- Conectar a la instancia EC2 mediante SSH
- Instalar **MySQL**
    > sudo apt-get install mysql-server
- Localizar el nombre del **host** de la **BBDD** en la consola de **AWS**
- Establecer una variable de entorno para el host **MySQL**
    > export MYSQL_HOST=[your-endpoint]
    - Encontrar el **endpoint**
    - En el panel de **AWS** y a la **Database** y seleccionar la correspondiente
    - Ir a **Connectivitiy & security** y consultar el **endpoint**
- Conectar con la base de datos **MySQL**
    > mysql --user=[Usuario] --password=[Contraseña] drupal
    - El usuario y la contraseña son los configurados en la base de datos de **RDS**
    - Si la conexión es correcta, la terminal indicará la conexión a la base de datos **MySQL**
- Crear un usuario para la base de datos de la aplicación de Drupal y otrtogar los permisos correspondientes
    > CREATE USER 'drupal' IDENTIFIED BY 'drupal-pass';  
    > GRANT ALL PRIVILEGES ON drupal.* TO drupal;  
    > FLUSH PRIVILEGES;  
    > exit
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
## Instalar y configurar Drupal
- Instalar PHP y sus dependencias
    > sudo apt-get install php  
    > sudo apt-get install php-dom php-gd php-simplexml php-xml php-opcache php-mbstring
- Descargar y descomprimir Drupal
    > wget https://www.drupal.org/download-latest/tar.gz  
    > sudo tar xf tar.gz -C /var/www/
- Copiar el directorio de *Drupal* a la raíz de *Apache* y modificar el nombre (Eliminar los números de la version para que sea más fácil trabajar con ello) 
    > sudo cp -r drupal-9.1.6/ html/drupal
- Reiniciar el servicio de *Apache*
    > sudo systemctl restart apache2.service
## Configurar el sitio de Drupal
- Ir a la dirección pública de la instancia y abrir *Drupal*
    > http://ec2-X-X-X-X.eu-west-3.compute.amazonaws.com/drupal
    - Cambiar las **X** por los números correspondientes
- Acceder al *asistente de configuración de Drupal*
- Elegir el *idioma* y pulsar **Save and continue**
- Elegir la opción **Estándar** y pulsar **Guardar y continuar**
- Configurar la base de datos
    - Escribir **drupal**
    - Escribir el usuario de la base de datos **drupal**
    - Escribir la contraseña de la **drupal_pass**
    - En configuración avanzada
    - Escribir el **endpoint** de la base de datos
- 


---
# Errores
## TRANSLATIONS DIRECTORY
- Error de directorio de traducciones
- Crear el directorio *sites/default/files/translations*
    > sudo mkdir /var/www/html/drupal/sites/default/files/translations
- Dar los permisos necesarios
    > sudo chmod 775 ./sites/default/files/translations/  
- Cambiar el usuario y el grupo 
    > sudo chown www-data:www-data files/translations/
- Reiniciar el servicio
    > sudo systemctl restart apache2.service
## FILE SYSTEM 
- Writable (public download method)
- Cambiar el usuario y el grupo a toda la carpeta **html/drupal**
    > sudo chown --recursive www-data:www-data /var/www/html/drupal
## SETTINGS FILE
- The Settings file is not writable.
- Cambiar el usuario y el grupo a toda la carpeta **html/drupal**
    > sudo chown --recursive www-data:www-data /var/www/html/drupal
## DATABASE SUPPORT
- Your web server does not appear to support any common PDO database extensions.
- Descargar la dependencia de mysql
    > sudo apt-get install php7.4-mysql
## CLEAN URLS
- Your server is capable of using clean URLs, but it is not enabled.
- Acttivar el mod **rewrite**
    > sudo a2enmod rewrite
## ERROR 1045 (28000)
- Access denied for user ‘root’@’localhost’ (using password: YES)
- Esto se debe a que por defecto el password de root para la base de datos no está fijado, así que lo vamos a crear nosotros con un comando
    > mysqladmin -u root password [newpassword]
## ERROR 2003 (HY000)
- Can't connect to MySQL server on 'drupal.cuyi3wlh14c5.eu-west-3.rds.amazonaws.com' (110)
- En grupos de seguridad, seleccionar el grupo correspondiente y pulsar en reglas de entrada.
- Añadir la regla
    - Todo el tráfico	Todo	Todo	::/0
---
# Bibliografía
- [https://aws.amazon.com/es/getting-started/hands-on/deploy-drupal-with-amazon-rds/](https://aws.amazon.com/es/getting-started/hands-on/deploy-drupal-with-amazon-rds/)

