# Más allá del cambio de contraseñas: Por qué una brecha en Active Directory persiste

Es un error común pensar que tras detectar una intrusión en el Directorio Activo (AD), un cambio masivo de contraseñas de usuario es suficiente para expulsar al atacante. En entornos empresariales complejos, los adversarios utilizan mecanismos de persistencia que sobreviven a la rotación de credenciales estándar.

## El problema de la persistencia profunda

Cuando un atacante obtiene privilegios elevados en un dominio de Windows, su objetivo es garantizar que, incluso si se cierran los puntos de entrada iniciales, puedan recuperar el acceso.

### 1. El ataque Golden Ticket (Ticket Granting Ticket)
El centro del problema suele residir en la cuenta **KRBTGT**. Esta cuenta es la que firma todos los tickets de Kerberos en el dominio.
* **El riesgo:** Si un atacante compromete el hash de la cuenta KRBTGT, puede generar sus propios tickets (Golden Tickets) con una duración de años y privilegios de administrador, sin necesidad de conocer la contraseña de ningún usuario real.
* **Solución técnica:** Cambiar las contraseñas de los usuarios no afecta al hash de KRBTGT. Se requiere rotar la contraseña de la cuenta KRBTGT **dos veces** para invalidar los tickets antiguos y sus derivados.

[Image of Kerberos authentication process and Golden Ticket attack]

### 2. Delegación no restringida y Silver Tickets
Los atacantes pueden configurar o abusar de la "Delegación de Kerberos" para suplantar identidades de servicio. 
* Los **Silver Tickets** se generan falsificando tickets de servicio (TGS) mediante el compromiso de la cuenta de una computadora o una cuenta de servicio específica.
* Al igual que con el Golden Ticket, cambiar la contraseña del usuario afectado no invalida el ticket de servicio ya emitido y en posesión del atacante.

## Puntos ciegos tras el compromiso

Incluso con contraseñas nuevas, un atacante puede haber dejado "puertas traseras" estructurales:

1.  **Modificación de ACLs (Listas de Control de Acceso):** El atacante puede haber modificado los permisos de un objeto en el AD para que su cuenta "normal" tenga permisos de escritura sobre el grupo de Administradores del Dominio.
2.  **Certificados de Usuario (AD CS):** Si la red utiliza Servicios de Certificado de Active Directory, un atacante puede haber solicitado un certificado de autenticación de larga duración. Los certificados no caducan ni se revocan simplemente cambiando la contraseña del usuario.
3.  **Scripts de Inicio y GPOs:** La alteración de Objetos de Directiva de Grupo (GPO) permite ejecutar código malicioso cada vez que cualquier usuario o servidor se inicie en la red.

## Estrategia de Remediación Efectiva

Para limpiar realmente un entorno de Active Directory tras una brecha, se deben seguir estos pasos técnicos:

* **Doble rotación de KRBTGT:** Es el paso crítico para invalidar el material de cifrado de Kerberos previo.
* **Auditoría de Derechos de Usuario:** Revisar el atributo `AdminCount` y los permisos sobre el contenedor `AdminSDHolder`.
* **Limpieza de Sesiones Activas:** Forzar el cierre de sesiones y purgar los tickets en memoria (LSASS) en servidores críticos.
* **Revisión de la Infraestructura de PKI:** Inspeccionar certificados emitidos recientemente y revocar aquellos sospechosos.

---
*Análisis técnico para administradores de sistemas y especialistas en respuesta a incidentes.*
