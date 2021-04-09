# AWS

- Es una plataforma en la nuve de virtualización

## Seguridad

### Identity and Access Management (IAM)

- los PRINCIPIOS especifican a QUIÉNES se les otorgan permisos.
- las ACCIONES especifican QUÉ es lo que se debe realizar.
- los RECURSOS especifican CUÁLES son las propiedades que se tienen que acceder.
El modelo zero trust a IAM significa adoptar el principio de mínimo privilegio. 
*Resumen*
- Las políticas de IAM determinan los límites de acceso para las entidades dentro de AWS
- Las políticas de IAM consisten en PRINCIPIOS, ACCIONES y RECURSOS
- Las políticas de IAM pueden utilizarse para aplicar el principio de mínimo privilegio
- IAM tiene varios tipos de políticas: las basadas en identidades y las basadas en recursos, por ejemplo
- IAM evalúa el acceso en función de la evaluación de todos los tipos de políticas aplicables a un determinado recurso.

### Seguridad en la red

La seguridad de la red abarca cualquier sistema, configuración o proceso que salvaguarde el acceso, la capacidad de uso y los recursos accesibles de la red.

Un enfoque de zero trust en la seguridad de la red implica un enfoque de defensa en profundidad que aplica controles de seguridad en todas las capas de la red

**Amazon Virtual Private Cloud (VPC)**
- Subredes: una serie de direcciones IP dentro de su VPC
- Tablas de enrutamiento: un conjunto de reglas que determinan hacia dónde se dirige el tráfico
- Gateway de Internet: un componente que permite la comunicación entre los recursos dentro de su VPC e Internet

Los grupos de seguridad son firewalls virtuales que puede utilizar a fin de controlar el tráfico que entra y sale de su recurso.

Además de las VPC, también puede utilizar AWS Web Application Firewall (WAF) para restringir aún más el tráfico en la red.

**Resumen**
- La seguridad de la red incluye mecanismos diseñados con el fin de salvaguarde el acceso, la capacidad de uso y los recursos accesibles de la red
- Un enfoque de zero trust en la seguridad de la red consiste en implementar una defensa en profundidad en todas sus capas
- VPC y WAF permiten aplicar medidas de seguridad a nivel de la red
Los grupos de seguridad permiten aplicar medidas de s- eguridad a nivel de recursos

### Cifrado de datos

Es el proceso de codificar la información de manera que sea ininteligible para cualquier tercero que no posea la clave que se requiere para descifrar los datos.

Adoptar un modelo zero trust para los datos significa cifrar todos nuestros datos, tanto en tránsito como en reposo.

**Cifrado de datos en tránsito**

Implica la codificación de los datos mientras viajan entre sistemas. Todos los servicios proporcionan HTTPS. También se ofrecen servicios como el balanceador de carga de aplicaciones (ALB)

**Cifrado de datos en reposo**

Implica cifrar los datos dentro de los sistemas.  La mayoría de estos servicios cuentan con el cifrado de datos activado de forma predeterminada. 

Los servicios de almacenamiento y bases de datos se integrna directaente con Amazon Key Service (KMS). Se trata de un servicio central de administración de claves que le permite crear claves administradas por el cliente (CMK) para cifrar los datos.

**Resumen**

- El cifrado de datos es el proceso mediante el cual se codifica la información de tal manera que solo quienes tengan la clave correcta puedan descifrar la información
- Todos los servicios de almacenamiento y base de datos en AWS proporcionan cifrado de datos en reposo y en tránsito
- Puede utilizar los servicios de la red de AWS como el ALB para aplicar el cifrado de datos en tránsito a sus propios servicios
- Puede utilizar una CMK para desbloquear funcionalidades avanzadas, como la creación de seguimientos de auditoría, el uso de claves personalizadas y la rotación automática de claves.

## Eficacia del rendimiento

Se centra en cómo puede ejecutar los servicios de manera eficiente y escalable en la nube. El aprovisionamiento es barato y rápido, lo que permite seleccionar el tipo de servidor que mejor se adapta a la carga de trabajo. Debido a que cada servidor es intercambiable y rápido de implementar, la capacidad se puede escalar rápidamente mediante el agregado de más servidores.

### Selección

Es la capacidad de elegir el servicio que más se alinea con la carga de trabajo. La carga de trabajo típica generalmente requiere la selección de alguna de las cuatro categorías principales:

- La **informática** involucra el servicio que procesará los datos (por ejemplo, máquina virtual)
- El **almacenamiento** involucra el almacenamiento estático de datos (por ejemplo, almacenamiento de objetos)
- La **base de datos** involucra el almacenamiento organizado de datos (por ejemplo, base de datos relacional)
- La **red** involucra la forma en que se mueven los datos (por ejemplo, red de entrega de contenido)

Independientemente de la categoría de servicio que elija, hay tres cosas que debe considerar:

**Tipo de servicio**

Cuando seleccione un **servicio de informática**, decida si desea una informática basada en máquinas virtuales, en contenedores o sin servidor:

- La informática basada en **máquinas virtuales** tiene el modelo mental más familiar para la mayoría de las personas, pero puede ser más costosa y requerir más mantenimiento
- La informática basada en **contenedores** permite una división más fina de la carga de trabajo y puede escalar rápidamente, pero incluye una configuración adicional y complejidad de organización
- La informática **sin servidor** elimina la mayoría de las complejidades de administración y escalado, pero tiene limitaciones estrictas de sistemas y requiere la adopción de nuevas cadenas de herramientas y procesos

Cuando seleccione un servicio de **almacenamiento**, decida si necesita almacenamiento de archivos, en bloque, de objetos o de archivado:

- Los servicios de almacenamiento en bloque, son excelentes para conservar datos de una sola instancia EC2.
- Los sistemas de archivos, son excelentes para dar acceso a múltiples clientes a los mismos datos.
- El almacenamiento de objetos, es excelente para grandes blobs de datos a los que los clientes necesitan acceder.
- El almacenamiento de archivos, es ideal para grandes cantidades de datos a los que se debe acceder con poca frecuencia.

Cuando seleccione un servicio de **base de datos**, decida si necesita una base de datos relacional, una base de datos no relacional, una solución de almacenamiento de datos o una solución de indexación y búsqueda de datos:

- Las bases de datos relacionales le permiten tener uniones y propiedades ACID, pero poseen un límite superior en el rendimiento y el almacenamiento de datos.
- Las bases de datos no relacionales tienen esquemas más flexibles y pueden escalar a límites mucho más altos que sus contrapartes relacionales, pero generalmente carecen de uniones y capacidades ACID completas.
- Las soluciones de almacenamiento de datos permiten análisis a gran escala a través del acceso rápido a petabytes de datos estructurados.
- Las soluciones de indexación y búsqueda de datos le permiten indexar y buscar datos de una amplia variedad de orígenes.

**Grado de administración**

La principal diferencia entre varios servicios de AWS del 
mismo tipo radica en su grado de administración.

Cuando se utiliza los servicios de **informática** se debe elegir entre:
- **EC2**: Proporciona mayor control, pero posee la administración mínima.
- **Lightsail**: Propociona una expereriencia mucho más administrada.
- **Elastic Beanstalk**: Se encuentra en el punto intermedio. Brinda un marco rígido para la arquitectura de su servicio, pero permite personalizarlo a través de la configuración. 

**Configuración**

La configuración depende de las características de rendimiento específicas que desea alcanzar.

Un buen lugar para empezar a buscar en los servicios **informáticos** es orientarse por sus requisitos informáticos y de memoria:
- Si se utiliza informática basada en **máquinas virtuales**, memoria y CPU se ven afectadas por el tamaño de su instancia.
- Si se utiliza informática basada en **contenedores**, memoria y CPU se pueden configurar individualmente.
- Si se utiliza informática **sin servidor**, solo se puede configurar directamente la memoria, el valor de los recursos del siestema aumenta linealmente a la cantidad de memoria disponible.

Dependiendo de las características de rendimiento para los servicios de **almacenamiento**:
- **Almacenamiento en bloque**
    - La latendia se ve afectada por la selección del tipo de volumen (HDD frente a SSD).
    - El rendimiento es proporcional al tamaño del volumen para la mayoría de tipos de volúmenes
    - La capacidad de IOPS es proporcional al tamaño del volumen para la mayoría de los tipos de volumen
- **Sistema de archivos**
    - La latencia y las IOPS se ven afectadas por su elección de modos de rendimiento.
    - El rendimiento se ve afectado por su opción de capacidad de rendimiento aprovisionado
- **Almacenamiento de objetos**
    - La latencia se ve afectada por la distancia geográfica al punto de enlace del bucket y la elección del método de recuperación
    - ñEl rendimiento se ve afectado por la optimización de la API, como carga de múltiples partes
    - IOPS no es configurable

Cuando evalúe la característica de rendimiento para los servicios de **base de datos**:
- **Relacional**
    - Las capacidades de recursos están determinadas por su elección de instancias EC2
- **No relacional**
    - Las capacidades de recursos están determinadas por opciones de configuración
- **Solución de almacenamiento de datos**
    - Las capacidades de recursos están determinadas por su elección de la instancia EC2
- **Solucción indexada**
    -   Las capacidades de recursos están determinadas por su elección de instancia EC2

**Resumen**
- La implementación de una carga de trabajo en AWS implica la selección de servicios mediante categorías de informática, almacenamiento, base de datos y red.
- En cada categoría puede seleccionar el tipo correcto de servicio en función de su caso de uso.
- En cada tipo, puede seleccionar el servicio específico en función de su grado de administración deseado.
- En cada servicio, puede seleccionar la configuración específica en función de las características de rendimiento que desea lograr.

### Escalado
Si bien elegir el servicio correcto es clave para comenzar, elegir como escala es importante para el rendimiento continuo.

**Escalado vertical**

Implica la actualización de la informática subyacente a un tipo de instancia más grande. Por ejemplo, supongamos que ejecuta una instancia t3.small. El escalado vertical de esta instancia puede ser actualizarla a t3.large.

El escalado vertical suele ser más fácil de implementar ya que lo puede hacer sin que el servicio esté en un clúster. La desventaja es que se encuentra con un límite superior mucho más bajo en comparación con el escalado horizontal.

**Escalado horizontal**

Implica aumentar el número de instancias subyacentes. Por ejemplo, supongamos que ejecuta una instancia t3.small. El escalado horizontal de esta instancia implicaría el aprovisionamiento de dos instancias t3.small adicionales.

Implica más sobrecarga en la implementación. Esto es porque necesita un servicio proxy para direccionar el tráfico a su flota de servicios. También necesita llevar a cabo comprobaciones de estado para eliminar las instancias defectuosas del grupo de direccionamiento, así como también seleccionar un algoritmo de direccionamiento específico que sea óptimo para la carga de trabajo. A cambio, obtendrá un servicio mucho más resistente que puede escalar a límites más altos en comparación con su contraparte de escalado vertical.

**Resumen**
- El escalado vertical es más sencillo operativamente, pero representa un riesgo de disponibilidad y posee límites más bajos
- El escalado horizontal requiere más sobrecarga, pero viene con mucha mejor fiabilidad y límites mucho más altos

## Fiabilidad

Se centra en cómo puede crear servicios que son resistentes a las interrupciones de infraestructura y servicio. 

Cuando se piensa en términos del radio de alcance, el problema del error ya no es una cuestión de si va a ocurrir, sino de cuándo va a suceder. Para afrontar un error cuando ocurre, se pueden utilizar las siguientes técnicas para limitar el radio de alcance:

1- Aislamiento de errores  
2- Límites

### 1- Aislamiento de errores

Limita el radio de alcance de un incidente mediante el uso de componentes independientes redundantes que se separan a través de zonas de aislamiento de errores. AWS tiene zonas de aislamiento de errores en tres niveles:

**Recurso y solicitud**

Los servicios de AWS dividen todos los recursos y solicitudes en una dimensión determinada. A estas particiones se las conoce como **celdas**. Las celdas están diseñadas para ser independientes y contener los errores dentro de una sola. AWS utiliza técnicas para limitar el radio de alcance. Todo esto sucede de forma transparente cada vez que se realiza una solicitud o se crea un recurso y no se requiere ninguna acción adicional de su parte.

**Zona de disponibilidad**  
Una zona de disponibilidad (AZ) de AWS es una instalación completamente independiente con capacidades dedicadas a la energía, el servicio y la red. El aislamiento de errores se logra a nivel de AZ mediante la implementación de instancias redundantes del servicio. 

**Región**  
Una región de AWS proporciona el aislamiento definitivo. Cada región es un centro de datos completamente autónomo, compuesto por dos o más AZ. Se consigue a nivel de región mediante la implementación de copias redundantes de los servicios en diferentes regiones de AWS.

**Resumen**
- Utilice zonas de aislamiento de errores para limitar el radio de alcance de las interrupciones del servicio o la infraestructura.
- El aislamiento de errores a nivel de recursos y solicitudes está incorporado en el diseño de cada servicio de AWS y no requiere acciones adicionales.
- El aislamiento de errores a nivel de AZ se logra mediante la implementación de los servicios a través de diversas AZ, lo que puede hacerse con un impacto mínimo de latencia.
- El aislamiento de errores a nivel de región se logra por medio de la implementación de los servicios a través de diversas regiones, lo que requiere una sobrecarga operacional considerable.

### 2- Límites
Los límites son restricciones que pueden aplicarse para proteger a los servicios de una carga excesiva. Son un medio eficaz para limitar el radio de alcance tanto de incidentes externos (DDoS) como internos.

AWS tienen límites específicos de servicio por cuenta y por región **(Cuotas de servicio)**. Existen dos tipos de límites:
- Límites blandos que se pueden aumentar si se solicita un aumento a AWS.
- Límites duros que no se pueden aumentar

Es importante monitorear los límites de servicio y saber cuándo se acerca al suyo a fin de evitar una interrupción. Para algunos recursos es posible realizar un seguimiento a través de CloudWatch, mientras que a otros hay que hacerlo de manera manual o por medio de scripts. 

**Resumen**
- Los límites son restricciones que pueden aplicarse para proteger a un servicio de una carga excesiva.
- Se pueden realizar seguimientos y administrar los límites de servicio de AWS mediante el servicio Service Quota.
- Hay límites blandos que se pueden aumentar y límites duros que no.

## Excelencia operativa   
El pilar de excelencia operativa se centra en cómo puede mejorar de manera continua su habilidad para ejecutar sistemas, crear mejores procedimientos y obtener información. Nos centraremos en los siguientes dos conceptos de excelencia operativa:

1. Infraestructura como código
2. Observabilidad

### 1. Infraestructura como código (IaC)
Es el proceso de administración de la infraestructura mediante archivos de configuración de lectura automática. La IaC es la base que permite automatizar la infraestructura.   
En lugar de aprovisionar servicios manualmente, se crean plantillas que describen los recursos que desea. La plataforma de IaC se encarga de aprovisionar y configurar los recursos.

La IaC ofrece una forma declarativa y automatizada de aprovisionar infraestructura. Permite aplicar a la infraestructura las mismas herramientas (Git) y procesos (revisión de código) que ya aplica al código.

La IaC en AWS implementó tradicionalmente mediante el servicio CloudFormation . CloudFormation requiere que declare los recursos mediante JSON o YAML.

**Resumen**
- La IaC es el proceso de administración de la infraestructura mediante archivos de configuración de lectura automática.
- La IaC es una forma declarativa y automatizada de aprovisionar infraestructura.
- Permite aplicar a la infraestructura las mismas herramientas y procesos que ya aplica al código.
- Utilice servicios como CloudFormation y CDK para implementar la IaC en AWS.

### 2. Observabilidad
Es el proceso de medición del estado interno del sistema. Por lo general se realiza con el objetivo de optimizarlo para que alcance un estado final deseado.

Crear una base sólida de observabilidad posibilita conocer el impacto de la automatización en el sistema y mejorarlo continuamente.Implementar la observabilidad incluye los siguientes pasos:

1. Recopilación
2. Análisis
3. Acción

**2.1. Recopilación**  
La recopilación es el proceso mediante el que se suman todas las métricas necesarias para evaluar el estado de un sistema. Se dividen en categorías.
- Métricas a nivel de **infraestructura**
    - Las emite automáticamente servicios de AWS y las recopila CloudWatch.
    - Algunos servicios también emiten registros estructurados que se pueden habilitar y recopilar con CloudWatch Logs.
- Métricas a nivel de **aplicación**
    - Las genera el software y las recopila las Métricas personalizadas de CloudWatch.
    - Los registros de software se pueden almacenar mediante CloudWatch Logs
- Métricas a nivel de **cuenta**
    - Las registra su cuenta de AWS y las recopila el servicio CloudTrail.

**2.2. Análisis**
La elección de la solución adecuada dependerá del caso de uso:
- Para analizar los registros almacenados en CloudWatch Logs, considere usar CloudWatch Logs Insight, un servicio que le permite buscar y analizar de manera interactiva sus datos de registro de Cloudwatch
- A fin de analizar los registros almacenados en S3, considere utilizar Athena, un servicio de consulta sin servidor
- A fin de analizar datos estructurados, considere utilizar RDS, un servicio de base de datos relacional administrado
- A fin de analizar grandes cantidades de datos estructurados, considere utilizar RedShift, un servicio de almacenamiento de datos en petabytes
- A fin de analizar datos basados en registros, considere utilizar Elasticsearch Service, una versión administrada de Elasticsearch, el conocido motor de análisis de código abierto.

**2.3. Acción**  
Una vez que haya recopilado y analizado las métricas, puede utilizarlas para lograr un resultado o proceso específico.

Ejemplos:
- Monitoreo y alarmas
    - Puede utilizar las Alarmas de CloudWatch para recibir notificaciones cuando un sistema haya incumplido el umbral de seguridad de una métrica específica
    - Esta alarma puede activar un mecanismo manual o automático de mitigación.
- Paneles
    - Con los Paneles de Cloudwatch puede crear paneles de sus métricas.
    - Con estos paneles puede registrar y, con el tiempo, mejorar el rendimiento del servicio
- Decisiones basadas en datos.
    - A fin de tomar decisiones basadas en datos, puede registrar los KPI de rendimiento y del negocio.

**Resumen**
- La observabilidad es el proceso de medición del estado interno del sistema para lograr un estado final deseado.
- La observabilidad consiste en recopilar métricas, analizarlas y tomar medidas en torno a ellas.

## Optimización de costos
El pilar de optimización de costos ayuda a lograr resultados empresariales mientra se minimizan los costos.  
Es útil considerar los gastos de la nube en términos de los gastos operativos en lugar de inversión de capital

El modelo de pago por uso introduce los siguientes cambios al proceso de optimización de costos:

1. Pago por uso
2. Optimización de costos del ciclo de vida

### 1. Pago por uso
Los servicios de AWS poseen un modelo de pago por uso en el que solo paga por la capacidad que utiliza. Hay cuatro maneras comunes de optimizar los gastos de la nube cuando paga por uso:

1. Tamaño correcto
2. Tecnología sin servidor
3. Reservas
4. Instancias de spot

**1.1 Tamaño correcto**  
El tamaño correcto hace referencia a la coincidencia entre el aprovisionamiento del servicio y la configuración para la carga de trabajo. Si los recursos informáticos están mayormente inactivos, considere utilizar una instancia EC2 más pequeña. Si la carga de trabajo requiere muchos recursos del sistema concretos, considere cambiar a una familia de instancias optimizada para ese recurso.

**1.2 Tecnología sin servidor**
solo paga por lo que utiliza. Si no se ejecuta por jemplo Lambda, no se le cobrará. La tecnología sin servidor es el mejor ejemplo de pago por uso.

**1.3 Reservas**
Implica comprometerse a pagar por cierta cantidad de capacidad a cambio de un descuento significativo.

**1.4 Instancias de spot**
Permiten aprovechar la capacidad de EC2 que no utiliza para ejecutar instancias con hasta un 90 % de descuento cuando se las compara con precios bajo demanda.

**Resumen**
- Los servicios de AWS se pagan por lo que usa: se le cobrará por la capacidad que utiliza
- Puede reestructurar las instancias a fin de ahorrar dinero en servicios que no coinciden con su carga de trabajo
- Puede utilizar tecnologías sin servidor para garantizar que solo pague cuando los clientes utilizan el servicio
- Puede usar reservaciones para obtener descuentos a cambio de un compromiso inicial
- Puede utilizar las instancias de spot para obtener descuentos por ejecutar cargas de trabajo tolerantes a errores










