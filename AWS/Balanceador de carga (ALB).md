# Balanceador de carga (ALB)
## 1. Configurar un balanceador de carga
- En la consola de **EC2** de **AWS** ir a **Balanceadores de carga**
- Pulsar en **Crear balanceador de carga**
- Seleccionar la opción que más le convenga, en este caso usaremos el **Balanceador de carga de aplicaciones (HTTP, HTTPS)** 
- Elegir el **Nombre** del balanaceador de carga
- Elegir el esquema, en este caso **expuesto a internet**
- En **Agentes de escucha** seleccionar el protocolo **HTTP** y el puerto **80**
- Marcar las **Zonas de disponibilidad**
- EL resto se deja por defecto y se pulsa **Siguiente: Configurar los ajustes de seguridad**
## 2. Configurar los ajustes de seguridad
- Dado que no se va aconfigurar el protocolo HHTPS, se salta al siguiente paso
- Pulsar **Seiguiente: Configurar grupos de seguridad**
## 3. Configurar grupos de seguridad
- Seleccionar un grupo de segurdad **existente**
- Para este caso se va a seleccionar el grupo por defecto **(default)** y el creado para drupal **(drupal)**
- Pulsar en **Siguiente: Configuración del enrutamiento**
## 4. Configuración del enrutamiento
- Elegir un **nombre** del grupo de destino, en este caso **drupalGrupoDestinoBC**
- Seleccionar en **Tipo de destino**, en este caso **Instancia**
- Pulsar en **Siguiente: Registrar destinos**
## 5. Registrar destinos
- **Red:** vpc-c426dcac(172.31.0.0/16)
- **Puerto:** 80 
- Pulsar en **Siguiente: Revisar**
## 6. Revisar
- Comprobar que todo sea correcto
- Pulsar en **Crear**
--- 
## Añadir el puerto de escucha 443
- En la consola de **AWS** ir al **Balanceador de carga**
- Seleccionar el *balanceador de carga* e ir a la pestaña de **Agentes de escucha**
- Pulsar en **Agregar agente de escucha** 
- En **Protocolo** seleccionar el **HTTPS:443**
- En **Acciones predeterminadas** pulsar en **Agregar acción** y seleccionar la opción **Reenviar a...**. En Grupo de destino seleccionar el grupo de destino creado anteriormente.
- En **Política de seguridad** seleccionar **ELBSecurityPolicy-FS-1-2-Res-2019-08**
- En **Certificado SSL predeterminado** seleccionar **Desde ACM (recomendado)** y el *DNS* creado.
- Pulsar en **Agregar agente de escucha**
---
## Redirigir el puerto 80 al 443
- En la consola de **AWS** ir a **Bañanceadores de carga**
- Seleccionar el balanceador e ir a la pestaña **Agentes de escucha**
- Seleccionar el **agente de escucha** del puerto **HTTP: 80** y después pulsar en **Editar**
- Pulsar en **+ Agregar acción** y seleccionar **Redirigir a...**
    - Seleccionar **HTTPS** y escribir **443**
    - Seleccionar **Usar host, ruta y consulta predeterminados...**
    - Seleccionar **301 - Movido permanentemente** y pulsar en el *check*
    - Pulsar en **Actualizar**

# Bibliografía
- [https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-application-load-balancer.html](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-application-load-balancer.html)

- [https://docs.aws.amazon.com/elasticloadbalancing/latest/application/tutorial-application-load-balancer-cli.html](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/tutorial-application-load-balancer-cli.html)

- [https://nadtakan-futhoem.medium.com/aws-load-balancer-503-service-temporarily-unavailable-e1e91c0dfcdb](https://nadtakan-futhoem.medium.com/aws-load-balancer-503-service-temporarily-unavailable-e1e91c0dfcdb)