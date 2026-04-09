# 🏢 BPO como Caballos de Troya: El caso de UNC6783 y el ataque a la cadena de suministro

Un reciente informe de inteligencia de amenazas ha identificado al grupo **UNC6783** como una amenaza creciente que utiliza a los proveedores de **Outsourcing de Procesos de Negocio (BPO)** como pasarelas (gateways) para infiltrarse en grandes corporaciones globales. Este cambio de táctica subraya una vulnerabilidad crítica: la confianza ciega en terceros que gestionan datos sensibles.

---

## 🔍 ¿Quién es UNC6783 y cómo opera?

UNC6783 no ataca directamente al objetivo final. En su lugar, compromete a las empresas que prestan servicios de soporte, contabilidad o RRHH a sus verdaderas víctimas.

### El flujo del ataque "Gateway":
1. **Compromiso Inicial**: El grupo infiltra a un proveedor de BPO mediante phishing dirigido o explotación de vulnerabilidades en sus accesos VPN/RDP.
2. **Explotación de la Confianza**: Una vez dentro del BPO, el atacante utiliza las conexiones legítimas (túneles VPN, cuentas de correo corporativas compartidas) para saltar a la red del cliente final.
3. **Persistencia y Exfiltración**: Al venir de una fuente "confiable", el tráfico malicioso suele evadir los controles de seguridad perimetral del cliente, permitiendo un robo de datos prolongado y silencioso.



---

## 📉 ¿Por qué los BPO son el objetivo perfecto?

* **Acceso Privilegiado**: Los empleados de BPO a menudo tienen acceso a sistemas internos, bases de datos de clientes y registros financieros para cumplir con sus funciones.
* **Seguridad Heterogénea**: A menudo, las empresas de outsourcing tienen presupuestos de ciberseguridad menores que las multinacionales para las que trabajan, convirtiéndolos en el "eslabón más débil".
* **Efecto Multiplicador**: Comprometer un solo BPO puede dar acceso a decenas de clientes corporativos simultáneamente.

---

## 🛡️ Estrategias de Defensa: Gestión de Riesgos de Terceros (TPRM)

Para los responsables de seguridad, este incidente obliga a replantear la relación con los proveedores:

1. **Zero Trust Network Access (ZTNA)**: No confiar en una conexión solo porque proviene de la IP de un socio. Cada acceso debe ser verificado individualmente.
2. **Monitoreo de Identidad**: Implementar alertas cuando las credenciales de un socio externo realizan acciones inusuales o acceden a datos fuera de su horario/alcance habitual.
3. **Auditorías de Seguridad Obligatorias**: Exigir a los BPO estándares mínimos (ISO 27001, SOC2) y realizar pruebas de penetración periódicas en sus puntos de acceso.
4. **Segmentación de Privilegios**: Limitar el acceso de terceros únicamente a las aplicaciones estrictamente necesarias para el servicio contratado.

---

## 🛠️ Tip de Verificación: Auditoría de Conexiones Externas

Si gestionas una infraestructura en la nube (Azure/AWS), puedes auditar qué identidades externas tienen permisos excesivos. En Azure AD, puedes listar usuarios invitados y sus roles:

```powershell
# Listar usuarios invitados y verificar sus roles asignados en Azure AD
Get-AzureADUser -Filter "UserType eq 'Guest'" | Select-Object DisplayName, UserPrincipalName, JobTitle
