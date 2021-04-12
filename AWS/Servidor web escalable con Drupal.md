# Servidor web escalable con Drupal y Lightsail

## 1. Crear una instancia en Lightsail  
1. Elegir **Crear instancia** en la pestaña de  **Instancias** de la página principal
1. Elegir la región de AWS y la zona de disponibilidad
1. Elegir la imagen (Tanto el sistema operativo como la aplicación)
1. Elegir un plan de instancia (RAM, SSD, CPU, MB...)
1. Escribir un nombre para la instancia
1. Crear la instancia

## 2. Conectarse a la instancia a través de SSH
1. En la pestaña **Instancias**, elegir el icono de la conexión rápida de SSH para la instancia de Drupal
2. Después de abrirse la ventana de cliente SSH ingresar el siguiente comando para recuperar la la contraseña predeterminada de la aplicación:
    > $HOME/bitnami_application_password
3. Apuntarse la contraseña que se muestra (Se usará más tarde para iniciar sesion).
4. *Elegir crear instancia*

## 3. Iniciar sesión en Drupal
1. En el navegador ir a *http://PublicIpAddress/user/login*
    - Remplazar *PublicIpAddress por la Ip d ela instancia* pública
2.  Iniciar sesión

## 4. Crear una IP estática y asociarla a Drupal
1. En la pestaña **Instancias**, elegir el icono de la conexión rápida de SSH para la instancia de Drupal
2. Elegir la pestaña **Redes (Networking)**, elegir **Crear IP estática)**
3. aLa ubicaciñon de la IP estática y la instancia se asociada se preseleccionan en función de la instancia elegida previamente.
4. Elegir el nombre de la IP estática y luego pulsar **Crear**

## 5. Crear la zona DNS y asignar un dominio a la instancia
1. En la pestaña de **Redes**, elegir **Crear zona DNS** 
2. Ingresar el dominio, luego elegir **Crear zona DNS**
3. Anotar la direcciñon del servidor de nombres que aparecen en la página
4. Después de que la administración de los registros DNS del dominio se tranfiera, agregar un registro para apuntar el vértice del dominio a la instancia de Drupal:
    - En la zona **DNS** del dominio elegir **Agregar registro**
    - En la casilla de Subdominiom ingregar el símbolo **@** para asignar el vértice del dominio a la instancia.
    - En la casilla de **Asignar**, elegir la IP estática que se asoción anteriormente.
    - Pulsar sobre **Guardar**
    - Esperar a que elcambio se propague a través del DNS antes de que el dominio comience a direccionar el tráfico a la instancia de Drupal

---
# Bibliografia

- [https://aws.amazon.com/es/getting-started/hands-on/build-drupal-website/](https://aws.amazon.com/es/getting-started/hands-on/build-drupal-website/)
