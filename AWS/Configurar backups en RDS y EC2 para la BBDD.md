# Configurar backups en RDS y EC2 para la BBDD
## Requisitos
- Configurar backups (snapshots) tanto de RDS como de el disco de la instancia ec2
- Para la BBDD hacerlo desde el servicio de RDS
- Amazon Data Lifecycle Manager
---
## Amazon Data Lifecycle Manager
- Se utiliza para automatizar la creación, retención y eliminación de instantáneas y AMI.
    - Proteger los datos con un programa de copias de seguridad regulares.
    - Crear AMI estandarizadas que se actualizar a intervalos regulares.
    - Conservar las copias de seguridad según se requieran
    - Reducir los costos de almacenamiento eliminando las copias obsoletas
    - Crear políticas de respaldo de recuperación de desastres que respalden los datos en cuentas aisladas
### **Instantáneas**
- Las instantáneas son el medio principal para realizar copias de seguridad de los datos de los volúmenes.
- Para ahorrar costos de almacenamiento, las instantáneas sucesivas son incrementales y contienen solo los datos de volumen que cambiaron desde la instantánea anterior.
- Cuando se elimina una instantánea en una serie de instantáneas para un volumen, solo se eliminan los datos que son exclusivos de esa instantánea. Se conserva el resto de la historia capturada del volumen.
### **AMI Respaldadas por EBS**
- Se pueden lanzar varias instancias desde una única AMI cuando se necesiten varias instancias con la misma configuración.
- Amazon Data Lifecycle Manager solo admite AMI respaldadas por EBS. 
- Las AMI respaldadas por EBS incluyen una instantánea para cada volumen de EBS que se adjunta a la instancia de origen.
### **Etiquetas de recursos de destino**
- Amazon Data Lifecycle Manager utiliza etiquetas para identificar los recursos a respaldar.
- Las etiquetas son metadatos personalizables que se pueden asignar a los recursos de AWS.
- Una política de Amazon Data Lifecycle Manager tiene como objetivo una instancia o volumen para la copia de seguridad mediante una sola etiqueta.
- Se pueden asignar varias etiquetas a una instancia o volumen si desea ejecutar varias políticas en él.
### **Políticas de ciclo de vida**
Una política de ciclo de vida consta de estas configuraciones básicas:
- **Tipo de política:** Define el tipo de recursos que se pueden administrar. mazon Data Lifecycle Manager admite dos tipos de políticas:
    - **instantáneas**: se utiliza para automatizar el ciclo de vida de las instantáneas de EBS. Estas políticas pueden apuntar a volúmenes e instancias de EBS.
    - **AMI respaldada por EBS**: se utiliza para automatizar el ciclo de vida de las AMI respaldadas por EBS. Estas políticas solo pueden apuntar a instancias.
    - **Política de eventos de copia entre cuentas**: Se utilizan oara automatizar la copia instantanea entre cuentas. Este tipo de política debe usarse junto con una política de instantáneas de EBS que comparta instantáneas entre cuentas.
- **Tipo de recusos**: Define el tipo de recursos a los que se dirige la política. Las políticas del ciclo de vida de las instantáneas pueden apuntar a instancias o volúmenes.
- **Etiquetas de destino**: Especifica las etiquetas que se deben asignar a un volumen de EBS o una instancia EC2 para que sea el destino de la política.
- **Horarios**: Las horas de inicio y los intervalos para crear instantáneas o AMI. Una política puede tener hasta cuatro horarios: un horario obligatorio y hasta tres horarios opcionales. **Importante**: La primera operación de creación de instantánea o AMI comienza una hora después de la hora especificada, las demás dentro de la hora programada.
- **Retención**: Especifica cómo deben conservarse las instantáneas o AMI. Se pueden retener según su recuento total o su edad. Cuando se alcanza el umbral de retención, se elimina la instantánea más antigua. 
- Ejemplos de politicas:
    - dministra todos los volúmenes de EBS que tienen una etiqueta con una clave de *account* y un valor de *finance*
    - Crea instantáneas cada *24 horas* a las *09:00 UTC*.
    - Comienza la creación de instantáneas a más tardar *09:59 UTC* cada día
    - Conserva solo las cinco instantáneas más recientes.
### **Programas de políticas**
- Los programas de las políticas definen cuándo se crean las instantáneas o AMI por la política. Las políticas pueden tener hasta cuatro programas: un programa obligatorio y hasta tres programas opcionales.
- Agregar varias programaciones a una sola política permite crear instantáneas o AMI en diferentes frecuencias utilizando la misma política. Por ejemplo creando una política única que cree instantáneas diarias, semanalaes, mensuales y anuales.
- Para cada programa, se puede definir la frecuencia, la configuración de restauración rápida de instantáneas, las reglas de copia entre regiones y las etiquetas.
- Cada programa se activa individualmente en función de su frecuencia. Si se activan varias programaciones al mismo tiempo, Amazon Data Lifecycle Manager crea solo una instantánea o AMI y aplica la configuración de retención de la programación que tiene el período de retención más alto.
---
## Bajar la retencción de los snapshots 
- En la consola de **AWS** ir a **Databases**
- Seleccionar la bases de datos y pulsar **Modify**
- Ir a **Backup** y modificar **Backup retention period**
- Cambiar la frecuencia, en este a **2 dias**
- Pulsar **Continuar**
- Seleccionar **Apply immediately**
- Pulsar **Modify DB instance**
---
## Configurar el Lifecycle para hacer backup de una instancia
- En la consola de **AWS** buscar **Lifecycle**
- En **Tipo de política** elegir **Política de instantáneas de EBS**
- Después seleccioanr **Instancia** 
- En **Descripción** escribir una breve descripción en la que se explique el objetivo de la política
- En **Destino con estas etiquetas** escribir la etiqueta con la que se indentifica la instancia a hacer backup
- En **Etiquetas de políticas** crear una nueva etiqueta
- El **Rol de IAM** dejar el **predeterminado**
- En **Programación de la política** cambiar el **nombre**, la **frecuencia**, **cada**cuento se realizan, **a partir** de que hora, el **tipo de retención** y cuantos backups se **retienen**
- Seleccionar **Indormación de etiquetado** y **Añadir una etiqueta**
- Dejar las opciones por defecto y pulsar en **Crear politica**





# Glosario
- **EBS:** Amazon Elastic Bloc Store. Proporciona volúmenes de almacenamiento a nivel de bloque para su uso con instancias EC2
- **AMI:** Amazon Machine Image. Proporcionan la información necesaria para lanzar una instancia
# Bibliografía
- [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html)
- [https://aws.amazon.com/es/blogs/storage/automating-amazon-ebs-snapshots-management-using-data-lifecycle-manager/](https://aws.amazon.com/es/blogs/storage/automating-amazon-ebs-snapshots-management-using-data-lifecycle-manager/)