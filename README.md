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
# ThereminESP - Requisitos y Plan de Testing

## 1. Introducción

El presente documento define los requisitos funcionales y no funcionales del sistema **ThereminESP**, así como el plan de pruebas y la plantilla de test cases que permitirán validar su correcto funcionamiento.

ThereminESP es un instrumento musical embebido que permite generar sonido en tiempo real mediante el movimiento de las manos del usuario, sin contacto físico, utilizando sensores ultrasónicos, síntesis digital de audio y una interfaz de visualización y monitoreo.

Este documento busca garantizar que cada funcionalidad del sistema esté claramente especificada, sea verificable mediante pruebas objetivas y pueda ser trazada dentro del proceso de desarrollo.

---

## 2. Requisitos Funcionales (RF)

### RF-01: Medición de distancia izquierda
El sistema deberá medir en tiempo real la distancia de la mano del usuario mediante el sensor ultrasónico izquierdo, en centímetros, dentro de un rango operativo de **5 cm a 80 cm**.

### RF-02: Conversión de distancia a frecuencia
El sistema deberá convertir la distancia medida por el sensor izquierdo en una frecuencia de audio, de manera que variaciones en la distancia produzcan cambios audibles en la nota generada.

### RF-03: Medición de distancia derecha
El sistema deberá medir en tiempo real la distancia de la mano del usuario mediante el sensor ultrasónico derecho, en centímetros, dentro del rango operativo de **5 cm a 80 cm**.

### RF-04: Control de timbre
El sistema deberá modificar el timbre del sonido generado en función de la distancia medida por el sensor derecho, permitiendo variaciones perceptibles en el sonido.

### RF-05: Generación de audio en tiempo real
El sistema deberá generar una señal de audio continua en tiempo real mientras se encuentre en operación.

### RF-06: Selección de forma de onda
El sistema deberá permitir seleccionar al menos tres formas de onda:
- Sinusoidal  
- Cuadrada  
- Triangular  
mediante botones físicos.

### RF-07: Visualización en OLED
El sistema deberá mostrar en la pantalla OLED:
- Frecuencia o nota generada  
- Forma de onda activa  
- Estado del sistema  

### RF-08: Sistema de logging
El sistema deberá emitir mensajes de logging por UART que incluyan:
- Timestamp  
- Nivel de severidad (INFO, WARN, ERROR)  
- Código de evento o error  

### RF-09: Detección de timeout de sensor
El sistema deberá detectar la ausencia de respuesta de los sensores ultrasónicos cuando no se reciba señal en el tiempo esperado.

### RF-10: Manejo de valores fuera de rango
El sistema deberá detectar valores fuera del rango válido de los sensores y descartarlos, manteniendo el último valor válido.

---

## 3. Requisitos No Funcionales (RNF)

### RNF-01: Comunicación I2C
El sistema deberá implementar comunicación I2C para la pantalla OLED con configuración documentada.

### RNF-02: Comunicación UART
El sistema deberá implementar comunicación UART a **115200 baud, 8N1** para logging y conexión con la GUI.

### RNF-03: Implementación física
El sistema deberá estar montado en tarjeta universal soldada o PCB, y no podrá presentarse en protoboard.

### RNF-04: Alimentación autónoma
El sistema deberá operar con una fuente de alimentación externa al laboratorio (batería o fuente propia).

### RNF-05: Carcasa funcional
El sistema deberá estar contenido en una carcasa funcional que permita su uso y proteja los componentes.

---

## 4. Plan de Testing

### 4.1 Objetivo
Validar que el sistema ThereminESP cumple todos los requisitos definidos mediante pruebas objetivas y verificables.

### 4.2 Alcance
Las pruebas cubrirán:
- Sensores ultrasónicos  
- Generación de audio  
- Selección de forma de onda  
- Visualización en OLED  
- Sistema de logging  
- Comunicación UART  
- Manejo de errores  
- Integración del sistema completo  

### 4.3 Tipos de prueba
Se utilizarán los siguientes tipos de pruebas:
- Pruebas funcionales  
- Pruebas de integración  
- Pruebas Hardware-in-the-loop (HIL)  
- Pruebas visuales  

### 4.4 Estrategia de pruebas
Cada requisito (RF y RNF) tendrá al menos un test case asociado que incluirá:
- Identificación del requisito  
- Objetivo de la prueba  
- Condiciones iniciales  
- Resultados esperados  
- Resultados obtenidos  
- Evidencia  

Esto permitirá posteriormente construir la matriz de trazabilidad (SRTM).

### 4.5 Evidencia
Las pruebas deberán estar respaldadas por evidencia como:
- Capturas de la GUI  
- Registros del monitor serial  
- Fotos del sistema  
- Videos de funcionamiento  
- Capturas de la pantalla OLED  

---

## 5. Plantilla de Test Cases

Se utilizarán los siguientes parámetros:

- **Test Case:** TC-XXX  
- **Estado:** Passed / Failed  
- **Requirement Traceability:** RF-XX / RNF-XX  
- **Test Objective:** descripción de lo que se desea verificar  
- **Preconditions:** condiciones necesarias antes de ejecutar la prueba  
- **Expected Results:** resultado esperado  
- **Actual Results:** resultado obtenido  
- **Evidence:** capturas, fotos o videos  

---

## 6. Lista Inicial de Test Cases

| Test Case | Requisito | Descripción |
|----------|----------|------------|
| TC-001 | RF-01 | Verificar medición de distancia sensor izquierdo |
| TC-002 | RF-02 | Verificar cambio de frecuencia según distancia |
| TC-003 | RF-04 | Verificar cambio de timbre con sensor derecho |
| TC-004 | RF-06 | Verificar cambio de forma de onda con botones |
| TC-005 | RF-07 | Verificar información mostrada en OLED |
| TC-006 | RF-08 | Verificar emisión de logs por UART |
| TC-007 | RF-09 | Verificar detección de timeout de sensor |
| TC-008 | RF-10 | Verificar manejo de valores fuera de rango |
| TC-009 | RNF-01 | Verificar comunicación I2C con OLED |
| TC-010 | RNF-02 | Verificar comunicación UART |

---


