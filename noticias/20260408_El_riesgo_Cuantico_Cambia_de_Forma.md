# 🌀 El Riesgo Cuántico cambia de forma: Por qué la urgencia es HOY

A menudo se habla del "Q-Day" (el día en que una computadora cuántica rompa el cifrado actual) como un evento lejano en el calendario. Sin embargo, análisis recientes de expertos como Joel Van Dyck sugieren que **el riesgo cuántico ha cambiado de forma, no de cronograma**. 

La amenaza ya no es una hipótesis futura, sino un problema de gestión de riesgos en el presente.

---

## 🛰️ El cambio de paradigma: "Cosechar ahora, descifrar después"

El mayor peligro actual no es que una computadora cuántica hackee tu banco mañana, sino la estrategia **SNDL (Store Now, Decrypt Later)**. 

* **¿En qué consiste?** Actores de amenazas (naciones-estado o grupos de cibercrimen organizado) están interceptando y almacenando enormes volúmenes de datos cifrados hoy.
* **El objetivo:** Esperar a que la tecnología cuántica madure lo suficiente para descifrar esa información en el futuro. 
* **La implicación:** Si tus datos tienen una vida útil o sensibilidad de 10 a 20 años (secretos de estado, registros médicos, propiedad intelectual), **ya están en riesgo hoy**.

## 🏗️ La infraestructura como punto crítico

El riesgo ha dejado de ser una preocupación solo para las criptomonedas o activos digitales para convertirse en un **riesgo sistémico de infraestructura**. 

1. **Protocolos heredados:** Muchos sistemas industriales y de defensa tienen ciclos de vida de décadas. Si se diseñan hoy con criptografía clásica (RSA/ECC), nacerán obsoletos.
2. **Dependencia de PKI:** La infraestructura de clave pública (PKI) que sostiene internet es el objetivo principal. El riesgo "cambió de forma" porque ahora entendemos que no solo fallará una aplicación, sino el modelo de confianza de toda la red.

---

## 💡 ¿Qué significa para los profesionales de seguridad?

La **agilidad criptográfica** es la única defensa real. No basta con esperar a que lleguen los estándares de NIST; las organizaciones deben:

* **Inventariar su criptografía:** Saber qué algoritmos están usando y dónde.
* **Evaluar la "longevidad" de sus datos:** Si la información debe ser secreta por más de 5 años, debe migrarse a algoritmos Post-Cuánticos (PQC) de inmediato.
* **Priorizar TLS y Firmas Digitales:** Los handshakes son los puntos más vulnerables a la interceptación masiva.

---

## 🛠️ Tip de Verificación: ¿Tu tráfico es vulnerable a SNDL?

Puedes usar herramientas de análisis de tráfico para identificar qué sesiones están utilizando algoritmos no resistentes a la computación cuántica (como RSA o ECDHE tradicional).

```bash
# Ejemplo usando 'sslyze' para identificar algoritmos de intercambio de claves
sslyze --resum --certinfo --sslv2 --sslv3 --tls1 --tls1_1 --tls1_2 --tls1_3 <dominio.com>
```

Análisis de resultados: Si el servidor solo soporta ECDHE o RSA sin extensiones híbridas (como las que ya están probando Google o Cloudflare), ese tráfico es susceptible de ser almacenado y descifrado en el futuro "Día Q".
