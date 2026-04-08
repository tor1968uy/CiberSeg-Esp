# 🛡️ La Hoja de Ruta hacia la Criptografía Post-Cuántica (PQC)

La transición hacia sistemas resistentes a la computación cuántica no es un simple cambio de "parche"; es una reingeniería completa de la confianza digital. Basándonos en los análisis de expertos en infraestructuras críticas, desglosamos los pilares de la **Criptografía Post-Cuántica (PQC)**.

---

## 🏗️ Los 3 Pilares de la Transición PQC

Para que una organización sea "Quantum-Ready", debe abordar tres frentes simultáneos:

### 1. Cripto-Agilidad (El "Cómo")
No se trata de elegir un algoritmo ganador, sino de diseñar sistemas que permitan intercambiar algoritmos sin necesidad de reescribir el software. 
* **Reto:** Los algoritmos PQC (como Kyber o Dilithium) tienen tamaños de llave y firmas mucho más grandes que RSA o ECC. Las infraestructuras actuales deben adaptarse para manejar este aumento de carga.

### 2. Algoritmos Basados en Retículos (Lattice-based)
La mayoría de los estándares seleccionados por el NIST se basan en problemas matemáticos de **retículos**. 
* **Por qué funcionan:** A diferencia de la factorización de números primos (que las computadoras cuánticas resuelven fácilmente con el Algoritmo de Shor), los problemas de retículos son extremadamente complejos de resolver incluso para una computadora cuántica a gran escala.

### 3. Implementación Híbrida
El consenso actual es no saltar al vacío. Se recomienda el uso de **Esquemas Híbridos**:
* Se combina un algoritmo clásico (como ECDHE) con uno post-cuántico.
* **Resultado:** Si el algoritmo PQC resulta tener una debilidad oculta, la seguridad clásica sigue protegiendo los datos. Si una computadora cuántica ataca, el algoritmo PQC mantiene la defensa.

---

## 📉 Comparativa: Criptografía Clásica vs. PQC

| Característica | Criptografía Clásica (RSA/ECC) | Criptografía Post-Cuántica (PQC) |
| :--- | :--- | :--- |
| **Base Matemática** | Factorización / Logaritmos | Retículos, Isogenias, Multivariables |
| **Resistencia Cuántica** | Vulnerable (Algoritmo de Shor) | **Resistente** |
| **Tamaño de Llave** | Pequeño (Eficiente) | Grande (Requiere optimización) |
| **Estado Actual** | Estándar Global | En proceso de estandarización (NIST) |

---

## 🛠️ Tip de Implementación: Probando Algoritmos PQC

Si quieres ver cómo se comporta un túnel TLS con algoritmos post-cuánticos, puedes utilizar la librería **Open Quantum Safe (OQS)**.

```bash
# Ejemplo de uso de 'openssl' con soporte OQS para probar una conexión Kyber
openssl s_client -connect <servidor-pqc>:443 -groups kyber768
```

¿Qué observar?
Al ejecutar este comando, notarás que el tiempo de negociación (handshake) puede variar ligeramente debido al tamaño de los paquetes. Es vital probar esto en entornos de QA antes de pasar a producción.

⚠️ Reflexión Final
La PQC no es una opción de lujo; es el nuevo estándar de higiene ciberespacial. Las organizaciones que ignoren la migración hoy, se encontrarán con una deuda técnica y de seguridad impagable en la próxima década.
