# Configurar vhost en Apache
- Limpir el host por defecto de Apache
- Configurar un nuevo vhost
- Objetvo: Al poner la IP, salga directamente el directorio de Drupal
---
- Copiar el archivo de configuración
    > sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/miWeb1.conf
- Editar el archivo
    > sudo vi /etc/apache2/sites-available/miWeb1.conf 

        <VirtualHost *:80> #Puerto donde escucha apache y desde donde sale la página
            ServerAdmin webadmin@dominio.com  #Correo del administrador del dominio
            ServerName dominio.com #Nombre del dominio
            ServerAlias www.dominio.com  #Alias del dominio, normalmente la www u otros
            DocumentRoot /var/www/html/drupal #El directorio donde se encuentra
            ErrorLog ${APACHE_LOG_DIR}/error.log  #El directorio para el log de error
            CustomLog ${APACHE_LOG_DIR}/access.log combined #El directorio para el log de acceso
        </VirtualHost>
- Activar el vhost sudo 
    > a2ensite miWeb1.conf  
- Deshabilitar el sitio por defecto     
    > sudo  /etc/apache2/sites-available/a2dissite 000-default.conf
- Reiniciar Apache
    > sudo systemctl restart apache2.service

    
# Biliografia
- [https://note-code.com/tutoriales/apache2/configurar-virtualhost](https://note-code.com/tutoriales/apache2/configurar-virtualhost)
- [https://www.icm.es/2020/06/06/vhosts-en-apache/](https://www.icm.es/2020/06/06/vhosts-en-apache/)