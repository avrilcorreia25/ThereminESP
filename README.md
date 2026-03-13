# 🎵 ThereminESP
### Sintetizador Gestual sin Contacto  
**Sistemas Embebidos · 2026-1**  
Universidad EIA · Escuela de Ingeniería y Ciencias Básicas

---

## 👥 Equipo

| Integrante | Rol |
|-------------|------|
| Avril Correia | Technical Lead |
| Matteo Paganessi | Firmware Engineer · Hardware Integration Engineer |
| Mariana Deossa | Verification & Testing Engineer |

---

# 1. ¿Qué es ThereminESP?

**ThereminESP** es un instrumento musical digital que se toca **sin contacto físico**.  
El usuario mueve sus manos en el aire frente a **dos sensores ultrasónicos** y el sistema genera sonido en tiempo real dependiendo de la posición de las manos.

El concepto está inspirado en el **Theremin**, un instrumento inventado en 1920 considerado el primer instrumento musical electrónico.  
ThereminESP es una versión moderna implementada con un **ESP32**.

---

# 2. ¿Cómo se usa?

| Acción del usuario | Qué hace el sistema |
|-------------------|---------------------|
| Mano izquierda cerca del sensor izquierdo | La nota sube (frecuencia más alta) |
| Mano izquierda lejos del sensor izquierdo | La nota baja (frecuencia más baja) |
| Mano derecha cerca del sensor derecho | Timbre brillante, sonido más agudo |
| Mano derecha lejos del sensor derecho | Timbre suave y oscuro |
| Botón A | Cambia la forma de onda a sinusoidal |
| Botón B | Cambia la forma de onda a cuadrada o triangular |

---

# 3. ¿Por qué es interesante para la demo?

- Es **muy intuitivo**: cualquier persona puede probarlo inmediatamente.
- El sonido cambia **en tiempo real con el movimiento de las manos**.
- Se pueden escuchar **diferentes formas de onda** claramente.
- La **pantalla OLED** muestra información del sistema.
- La **GUI en PC** permite ver logs y eventos del sistema en vivo.

---

# 4. Definición del Problema

Los instrumentos musicales tradicionales requieren **contacto físico preciso y entrenamiento prolongado**. Además, muchos sistemas musicales comerciales son **cerrados y poco flexibles para aprendizaje o personalización**.

La generación de sonido en tiempo real en sistemas embebidos implica múltiples desafíos:

- adquisición precisa de datos de sensores
- procesamiento de señales en tiempo real
- comunicación entre periféricos
- visualización de información al usuario
- ejecución dentro de recursos limitados de un microcontrolador

---

## Problema a resolver

Diseñar e implementar un **instrumento musical gestual embebido** que permita generar y controlar sonido en tiempo real mediante el movimiento de las manos, integrando:

- sensores ultrasónicos
- síntesis digital de audio
- visualización en pantalla
- comunicación con una interfaz gráfica en PC

todo ejecutándose en hardware embebido **de bajo costo y portátil**. :contentReference[oaicite:0]{index=0}

---

# 5. Alcance del Proyecto

## Incluido en el alcance

- Firmware en **C/C++ sobre ESP32**
- Lectura de distancia con **2 sensores HC-SR04**
- Síntesis digital de audio con ondas:
  - sinusoidal
  - cuadrada
  - triangular
- Control de timbre en tiempo real
- Selección de onda con **botones físicos**
- Pantalla **OLED SSD1306**
- Amplificador de audio **PAM8403**
- Sistema de **logging estructurado**
- GUI en **Python (Tkinter)** para monitoreo
- Hardware soldado en tarjeta universal
- Alimentación con **batería LiPo**
- Documentación técnica completa

## Fuera del alcance

- Grabación de sesiones musicales
- Bluetooth o WiFi
- Reconocimiento automático de melodías
- Aplicación móvil

---

# 6. Objetivo General

Desarrollar un **instrumento musical gestual embebido basado en ESP32** que genere audio en tiempo real a partir de la posición de las manos capturada por sensores ultrasónicos.

---

# 7. Objetivos Específicos

- Implementar medición de distancia con sensores ultrasónicos.
- Desarrollar síntesis digital de audio con múltiples formas de onda.
- Diseñar un sistema de logging con timestamps y niveles de severidad.
- Construir una GUI en Python para monitoreo del sistema.
- Diseñar el hardware y la carcasa del dispositivo.
- Construir una **SRTM** con requisitos y casos de prueba.

---

# 8. Hardware del Sistema

| Componente | Función |
|-------------|--------|
| ESP32 DevKit v1 | Microcontrolador principal |
| HC-SR04 (x2) | Sensores ultrasónicos |
| OLED SSD1306 | Pantalla de estado |
| PAM8403 | Amplificador de audio |
| Bafle externo | Reproducción de sonido |
| Botones | Selección de forma de onda |
| Batería LiPo | Alimentación portátil |
| TP4056 | Módulo de carga |

Costo aproximado de componentes: **~20 USD**

---

# 9. Arquitectura del Sistema

El sistema se divide en módulos de firmware:

| Módulo | Función |
|------|------|
| Sensor | Lectura de distancia |
| Síntesis | Generación de onda |
| Filtro | Control del timbre |
| Display | Actualización de OLED |
| Logging | Registro de eventos |
| Waveform | Cambio de forma de onda |

---


