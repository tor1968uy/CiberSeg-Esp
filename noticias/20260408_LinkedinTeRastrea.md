# 🚨 Alerta de Privacidad: ¿LinkedIn espía a sus usuarios mediante scripts?

Recientes investigaciones, de las que se hace eco *El Chapuzas Informático*, han puesto bajo la lupa las prácticas de recopilación de datos de **LinkedIn**. Se informa que la plataforma estaría utilizando scripts avanzados para recopilar información detallada del comportamiento y hardware de los usuarios, incluso más allá de lo estrictamente necesario para el funcionamiento de la red social.

---

## 🕵️ ¿Qué está ocurriendo técnicamente?

El informe sugiere que LinkedIn utiliza técnicas de **Canvas Fingerprinting** y rastreo de telemetría que permiten identificar de forma única a un usuario sin necesidad de cookies tradicionales.

### Los puntos clave del informe:
1. **Recopilación de metadatos de hardware**: Los scripts analizan la resolución de pantalla, fuentes instaladas, versión del sistema operativo y hasta el nivel de batería.
2. **Seguimiento del cursor y comportamiento**: Se monitoriza el movimiento del ratón y el tiempo de permanencia en elementos específicos para alimentar sus algoritmos de recomendación y publicidad.
3. **Persistencia**: Al basarse en características únicas del navegador (fingerprint), es extremadamente difícil de bloquear mediante el simple borrado de cookies.

---

## 🛡️ Implicaciones para el Profesional de Ciberseguridad

Para quienes trabajamos en seguridad, esto representa un riesgo de **OSINT (Open Source Intelligence)**. 
* Un atacante que logre comprometer o interceptar estos flujos de datos podría obtener un perfil técnico exacto de la máquina de un empleado.
* Facilita ataques de **Spear Phishing** mucho más creíbles al conocer el entorno exacto del objetivo.

---

## 🛠️ Tip de Protección: ¿Cómo mitigar el Fingerprinting?

Si quieres navegar de forma más privada en LinkedIn y otros sitios similares, aquí tienes algunas herramientas y técnicas:

### 1. Extensiones de Navegador
* **uBlock Origin**: Configurado en modo avanzado para bloquear scripts de rastreo de terceros.
* **CanvasBlocker**: Específicamente diseñado para alterar los datos que el navegador entrega a los scripts de fingerprinting.

### 2. Uso de Navegadores enfocados en Privacidad
Navegadores como **Brave** o **LibreWolf** bloquean estas técnicas de forma nativa.

### 3. Comprobación de tu huella digital
Puedes verificar qué tanta información está filtrando tu navegador actual en sitios como:
* [Cover Your Tracks (EFF)](https://coveryourtracks.eff.org/)
* [AmiUnique](https://amiunique.org/)

---

## 💻 Ejemplo de Script: Detectando el rastreo
En tu sección de `/codigo`, podrías añadir este pequeño script de consola para detectar si un sitio está intentando leer datos de tu canvas (técnica común de fingerprinting):

```javascript
// Monitorizar intentos de lectura de Canvas (Fingerprinting simple)
const originalGetImageData = CanvasRenderingContext2D.prototype.getImageData;
CanvasRenderingContext2D.prototype.getImageData = function() {
    console.warn("⚠️ ¡Alerta! El sitio web está intentando leer datos del Canvas (posible Fingerprinting).");
    return originalGetImageData.apply(this, arguments);
};
```


⚠️ Conclusión
Aunque LinkedIn defienda estas prácticas como "mejoras de seguridad y experiencia de usuario", la línea entre la funcionalidad y el espionaje corporativo es muy delgada. En un repositorio de ciberseguridad, nuestra misión es concienciar sobre la importancia de la higiene digital.
