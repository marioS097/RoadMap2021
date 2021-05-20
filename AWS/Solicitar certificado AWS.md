# Solicitar un certificado
- En la consola de **AWS** buscar **Certificate Manager**
- Seleccionar la opción **Aprovisar**
- Pulsar en **Solicitar un certificado**
## Paso 1: Agregar nombres de dominio
- Agregamos el nombre del dominio del balanceador de carga. En este caso el *drupalBC-10xxx.eu-west-3.elb.amazonaws.com*
- Pulsar en **Siguiente**
## Paso 2: Seleccionar un método de validación
- Seleccionar **Validación de DNS**
- Pulsar en **Siguiente**
## Paso 3: Agregar etiquetas
- Agregar una etiqueta (Es opcional)
- En este caso añadiremos una: **EtiquetaCertificado :  CertificadoDnsDrupal**
- Pulsar en **Revisar**
## Paso 4: Revisar
- Comprobar que todos los datos sean correctos
- Pulsar en **Confirmar y solicitar**