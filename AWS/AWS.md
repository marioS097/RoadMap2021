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

*Amazon Virtual Private Cloud (VPC)*
- Subredes: una serie de direcciones IP dentro de su VPC
- Tablas de enrutamiento: un conjunto de reglas que determinan hacia dónde se dirige el tráfico
- Gateway de Internet: un componente que permite la comunicación entre los recursos dentro de su VPC e Internet

Los grupos de seguridad son firewalls virtuales que puede utilizar a fin de controlar el tráfico que entra y sale de su recurso.

Además de las VPC, también puede utilizar AWS Web Application Firewall (WAF) para restringir aún más el tráfico en la red.

*Resumen*
- La seguridad de la red incluye mecanismos diseñados con el fin de salvaguarde el acceso, la capacidad de uso y los recursos accesibles de la red
- Un enfoque de zero trust en la seguridad de la red consiste en implementar una defensa en profundidad en todas sus capas
- VPC y WAF permiten aplicar medidas de seguridad a nivel de la red
Los grupos de seguridad permiten aplicar medidas de s- eguridad a nivel de recursos


