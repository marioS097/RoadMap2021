# Función de Lambda
- Crear una función Lambda para apagar/encender el servidor web automáticamente a en un horario determinado. Por ejemplo, de Lunes a Viernes de 8:00 a 17:30
---
## Crear la política y el rol en IAM
- En la consola de **AWS** ir a **IAM**
- Ir a **Políticas** y pulsa en **Crear una política**
- Seleccionar **JSON** y copiar el código  

    ```
    {
    "Version": "2012-10-17",
    "Statement": [
        {
        "Effect": "Allow",
        "Action": [
            "logs:CreateLogGroup",
            "logs:CreateLogStream",
            "logs:PutLogEvents"
        ],
        "Resource": "arn:aws:logs:*:*:*"
        },
        {
        "Effect": "Allow",
        "Action": [
            "ec2:Start*",
            "ec2:Stop*"
        ],
        "Resource": "*"
        }
    ]
    }
    ```
- Pulsar en **Siguiente: Etiquetas** 
- **Agregar etiquetas** (Opcional)
    - En este caso se pondrá: **EtiquetaPolitica - startStop**
- Pulsar en **Siguiente: Revisar**
- Escribir un **nombre** para la política
- Pulsar en **Crear una política**
- Una vez creada la **política** hay que crear el **rol**
- Dentro de **IAM** ir a **Roles**
- Pulsar sobre **Crear un rol**
- En **Servicio de AWS** seleccionar el caso común **Lambda** y pulsar en **Siguiente: Permisos**
- Buscar la *política* creada anteiormente y pulsar en **Siguiente: Etiquetas**
- **Añadir etiquetas** (Opcional)
    - En este caso: **EtiquetaRol - startStop**
- Pulsar **siguiente: Revisar**
- Escribir un **Nombre del rol** y una **Descripción del rol** (Opcional)
- Para terminar pulsar en **Crear un rol**

## Crear las funciones Lambda
- En la consola de **AWS** buscar el servicio **Lambda**
- Ir a **Funciones** y pulsar sobre **Crear una función**
- Seleccionar **Crear desde cero**
- Escribir el **nombre** que se le vaya a dar a la función
- En **Tiempo de ejecución** seleccionar **Python 3.8**
- Desplegar **Cambiar el rol de ejecución predeterminado**
    - Seleccionar la opción **Uso de una existente** y seleccionar el **rol** creado anteriormente
- Pulsar en **Crear una función**
- Ir al servicio **Lambda**, **Funciones**
- Seleccionar la función creada e ir a la pestaña **Código** y copiar el siguiente código
    ```
    import boto3
    region = 'REGION'
    instances = ['ID-INSTANCIA']
    ec2 = boto3.client('ec2', region_name=region)

    def lambda_handler(event, context):
        ec2.stop_instances(InstanceIds=instances)
        print('stopped your instances: ' + str(instances))

    ``` 
    - **Importante**: Remplazar tanto la **región** como el **ID-INSTANCIA** por las propias
- Seleccionar la pestaña **Configuración** ir a **Configuración general** y pulsar sobre **Editar**
- Cambiar el **Tiempo de espera** a **10 min** y pulsar en **Guardar**
- Ir a **Acciones** y seleccionar **Publicar nueva versión**, escribir una **Nota** (Opcional)
- Volver a **Crear una función** pero cambiando el **Código**
    ```
    import boto3
    region = 'eu-west-3'
    instances = ['i-040f3ce432493622d']
    ec2 = boto3.client('ec2', region_name=region)

    def lambda_handler(event, context):
        ec2.start_instances(InstanceIds=instances)
        print('started your instances: ' + str(instances))
    ```
    - **Importante**: Remplazar tanto la **región** como el **ID-INSTANCIA** por las propias
- Ir a **Acciones** y seleccionar **Publicar nueva versión**, escribir una **Descripción** (Opcional)
## Comprobar las funciones Lambda (EN PROCESO)
- En la consola de **AWS** buscar el servicio **Lambda**
- Ir a **Funciones** y seleccionar una de las funciones creadas
- En la pestaña **Código** pulsar el botón **Test**
- Seleccionar **Crear un evento de prueba nuevo**, en plantilla seleccionar **Amazon CloudWatch**
- Escribir un **Nombre** y pulsar en **Crear** (El *JSON* dejarlo como esté)
- Pulsar en **Test** y comprobar que sale una nueva pestaña con el nombre del evento
- Repetir con la otra **función**
## Crear reglas de CloudWatch Events que activen las funciones Lambda
- En la consola de **AWS** ir a **CloudWatch**
- Ir a **Eventos** y seleccionar **Reglas**
- Pulsar en **Crear una regla**
- En **Origen del evento** seleccionar **Programación**
- Seleccionar **Expresión Cron**
    - Para que se enciendan las maquinas de *Lunes* a *Viernes*  a las *8* escribir está **expresión Cron**
        > 0 6 ? * MON-FRI *
- En **Destinos** pulsar sobre **Añadir destino**
- Selecionar **Función Lamda** y en **Función** la función creada anteriormente para levantar la instancia
- Pulsar en **Configurar los detalles**
- Escribir el **Nombre** de la regla, en **Descripción** añadir una pequeña descripción a la regla *(Opcinal)* y marcar el **Estado Habilitado**
- Pulsar en **Crear una regla**
- Repetir para crear la regla de apagado
    - Utilizar la siguiente **expresión Cron**
        > 30 15 ? * MON-FRI *
    - Seleccionar la **Función Lambda** para detener instancias

---
# Bibliografía
- [https://aws.amazon.com/es/premiumsupport/knowledge-center/start-stop-lambda-cloudwatch/](https://aws.amazon.com/es/premiumsupport/knowledge-center/start-stop-lambda-cloudwatch/)
- [https://aws.amazon.com/es/lambda/features/](https://aws.amazon.com/es/lambda/features/)
- [https://docs.aws.amazon.com/es_es/lambda/latest/dg/services-cloudwatchevents-tutorial.html](https://docs.aws.amazon.com/es_es/lambda/latest/dg/services-cloudwatchevents-tutorial.html)
- [https://aws.amazon.com/es/cloudwatch/pricing/](https://aws.amazon.com/es/cloudwatch/pricing/)
