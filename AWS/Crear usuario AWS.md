# Crear usuarios en AWS 
## Preequisitos
- Tener en el teléfono móvil una aplicación para la autentificación en dos pasos  
    - Google autenticador
    - AUTI
---
## Crear usuario
1. En la consola de **AWS** ir a **IAM**
2. En el panel de navegación seleccionar **usuarios** luego pulsar en **Añadir usuario(s)**  
    1. Elegir el **nombre de usuario**   
    2. Seleccionar la opción **Acceso a la consola de administración de AWS** 
    3. Elegir la **contraseña de la consola** ya sea *generada automáticamente* o crear una *contraseña personalizada*
    4. Elegir si el usuario va a *restablecer la contraseña en el prózimo inicio de sesión*
    5. Pulsar en **Siguiente: Permisos**
3. En **Establecer permisos** elegir la opción **Añadir un usuario al grupo**
    1. Seleccionar **Crear un grupo**
    2. Escribir el **nombre del grupo**
    3. Seleccionar la pólitica **AdministratorAccess**
    4. Pulsar en **Crear un grupo**
    5. Seleccionar el grupo creado
    6. Pulsar en **Siguiente: Etiquetas**
4. Añadir etiquetas **(Opcional)**
    1. Clave: EtiquetaUsuario
    2. Valor: UsuarioAdministradorMario
    3. Pulsar en **Siguiente: **Revisar**
5. Comprobar que los datos sean correctos y pulsar en **Crear un usuario**
6. Descargar el *.csv* si se ve oportuno y pulsar en **Cerrar**
## Añadir la autentificación en dos pasos
1. Pulsar en el usuario
2. Ir a la pestaña de **Credenciales de seguridad**
3. En la opción **Dispositivo MFA asignado** pulsar en **Administración**
    1. Con la opción **Dispositivo MFA virtual** seleccionada, pulsar en **Continuar**
    2. Pulsar en **Mostrar el código QR**
    3. Desde el móvil ir a la aplicación de seguirdad y pulsar en añadir, luego seleccionar la opción escanear QR.
    4. La aplicación ira generando códigos de 6 dígitos, escribir dos códigos consecutivos y pulsar en **Aceptar**
# Bibliografía
- [https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html)