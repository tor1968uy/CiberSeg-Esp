# ⚡ Rowhammer 2.0: Ataques de memoria logran el control total de sistemas con GPUs NVIDIA

Un grupo de investigadores de seguridad ha demostrado una nueva variante del clásico ataque **Rowhammer** que, por primera vez, permite obtener privilegios de superusuario (root) aprovechando la interacción entre la CPU y las GPUs de NVIDIA. 

Este descubrimiento rompe la creencia de que las protecciones actuales de la memoria eran suficientes para aislar los procesos del sistema de las operaciones de la tarjeta gráfica.

---

## 🔍 ¿Qué es Rowhammer y qué hay de nuevo?

El ataque **Rowhammer** tradicional consiste en "martillear" (leer/escribir repetidamente) una fila de celdas de memoria DRAM para provocar fugas de carga eléctrica que alteren los bits de las filas adyacentes (*bit-flipping*). 

### La novedad técnica:
Hasta ahora, Rowhammer se ejecutaba principalmente desde la CPU. Sin embargo, este nuevo ataque utiliza la **GPU de NVIDIA** para realizar el martilleo a una velocidad y precisión mucho mayores. 

1. **Aislamiento roto**: Al usar la GPU, los atacantes pueden evadir las defensas basadas en software que monitorizan los accesos a la memoria desde la CPU.
2. **Control Total**: Mediante la manipulación precisa de bits en la memoria física, los investigadores lograron corromper estructuras de datos críticas del núcleo (kernel), permitiendo que un proceso sin privilegios tome el control total de la máquina.
3. **Hardware afectado**: El ataque ha sido validado en sistemas modernos que utilizan memoria DDR4 y GPUs con arquitectura Turing y Ampere.

---

## 💡 ¿Por qué es crítico para la comunidad?

Este ataque no es solo una curiosidad académica. Sus implicaciones son profundas:

* **Entornos de IA y Computación en la Nube**: Muchos servidores en la nube comparten GPUs entre diferentes usuarios. Un atacante podría, teóricamente, escapar de su entorno virtual y comprometer el servidor físico o los datos de otros clientes.
* **Persistencia**: Al ser un fallo de hardware (física de semiconductores), no existe un "parche de software" sencillo que lo elimine sin degradar seriamente el rendimiento de la memoria.
* **Evasión de EDR**: La mayoría de las herramientas de detección (EDR) no monitorizan el tráfico interno de la memoria RAM provocado por comandos de bajo nivel de la GPU.

---

## 🛠️ Tip de Auditoría: ¿Cómo saber si tu RAM es vulnerable?

Aunque este ataque específico requiere herramientas de investigación, puedes comprobar la susceptibilidad de tu memoria a ataques Rowhammer genéricos con herramientas de código abierto como `dmidecode` para ver si tu RAM tiene **ECC (Error Correction Code)**.

### Comando de verificación (Linux):
```bash
# Verificar si la memoria RAM soporta ECC (lo cual mitiga parcialmente Rowhammer)
sudo dmidecode -t memory | grep -i "Error Correction Type"
