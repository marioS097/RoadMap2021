# Drush
## Información
- Drush es una impresionante interfaz de shell para la gestión y administración de Drupal directamente desde la línea de comandos de su servidor. Es una herramienta muy útil ya que le ayuda a realizar varias tareas de administración utilizando sólo uno o dos comandos en el terminal, reemplazando la necesidad de muchos clics y refrescos de página en la interfaz de usuario. 
## Instalaccion
- Instalar comando **composer**
    > curl -sS https://getcomposer.org/installer | php  
    > sudo mv composer.phar /usr/local/bin/composer
- Instalar drush con las dependencias
    > composer global require drush/drush:8.* -W
- Agreguar la ruta del compositor a la ruta *(.bashrc)*
    > export PATH="$HOME/.config/composer/vendor/bin:$PATH"
## Comandos útiles
- Limpiar la caché de Drupal 
    - En el directorio donde esté instalado **Drupal**
    > drush cr
# Bibliografia
- [https://www.drupal.org/node/1248790](https://www.drupal.org/node/1248790)