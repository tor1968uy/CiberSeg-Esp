# 📢 Alerta: Java elimina criptografía obsoleta en actualizaciones de JDK

La evolución del ecosistema Java continúa priorizando la seguridad por encima de la compatibilidad con sistemas legados. Las actualizaciones más recientes del **Java Development Kit (JDK)** introducen cambios de ruptura que impactan directamente en cómo se establecen conexiones seguras.

---

## 🔍 Detalles Técnicos de los Cambios

La eliminación de algoritmos obsoletos se ha materializado en dos frentes críticos:

### 1. Deshabilitación de RSA Key Exchange (`JDK-8245545`)
Los esquemas de intercambio de llaves basados en RSA (donde la llave pública del servidor se usa para cifrar el secreto pre-maestro) se consideran ahora inseguros debido a la falta de **Forward Secrecy** (Secreto Perfecto hacia Adelante).

* **El cambio:** Están deshabilitados por defecto.
* **Impacto:** Si un atacante captura el tráfico hoy y consigue la llave privada del servidor en el futuro, podría descifrar todas las comunicaciones pasadas. Al deshabilitarlo, Java obliga al uso de **Diffie-Hellman (DHE o ECDHE)**.

### 2. Adiós a SHA-1 en Handshakes TLS (`JDK-8340321`)
SHA-1 ha sido considerado criptográficamente débil durante años debido a su vulnerabilidad a colisiones.

* **El cambio:** Se ha desactivado por defecto en las firmas de los "handshakes" para los protocolos **TLS 1.2** y **DTLS 1.2**.
* **Contexto:** Aunque TLS 1.2 sigue siendo seguro, el uso de SHA-1 dentro de este protocolo para autenticar el intercambio de mensajes ya no se considera aceptable bajo estándares modernos.

---

## 💡 ¿Qué significa esto en la práctica?

Para muchos administradores y desarrolladores, esto no es solo una actualización; es un posible **punto de quiebre operativo**:

* **Fallas de conexión:** Aplicaciones que antes conectaban con bases de datos antiguas o balanceadores de carga obsoletos lanzarán excepciones de tipo `SSLHandshakeException`.
* **Riesgo de estancamiento:** Las organizaciones podrían optar por no actualizar el JDK para no "romper" el sistema, quedando expuestas a vulnerabilidades críticas en otros componentes del runtime.
* **Invisibilidad:** Estos errores suelen aparecer en procesos de backend o tareas programadas que no siempre cuentan con monitoreo en tiempo real.

---

## 🛠️ Tip Técnico: ¿Cómo verificar si mis sistemas son afectados?

Antes de actualizar tu parque de servidores JDK, puedes auditar tus servicios externos o internos para ver si dependen de estos algoritmos débiles.

### Usando Nmap
Puedes listar las suites de cifrado soportadas por un servidor para verificar si todavía ofrece `TLS_RSA_...` (vulnerable al cambio) o si requiere firmas SHA-1:

```bash
# Escanear un servidor para ver sus algoritmos de cifrado
nmap --script ssl-enum-ciphers -p 443 <IP_O_DOMINIO>
```
¿Qué buscar en los resultados?

Si ves suites que comienzan con TLS_RSA_WITH_..., esas dejarán de funcionar.

Busca firmas que mencionen sha1. Si son las únicas disponibles, la conexión fallará con los nuevos JDK.
