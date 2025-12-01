# ⚙️ Plataforma de Simulación HIL para Sistemas Dinámicos con LaunchPad C2000

Este repositorio contiene el código fuente, modelos de simulación y scripts de configuración desarrollados para el trabajo de grado titulado:

_"Implementación de Sistemas Dinámicos mediante Simulación HIL con la Tarjeta LaunchPad C2000: Un Enfoque para la Educación en Ingeniería"_

El proyecto presenta una plataforma educativa de bajo costo para realizar simulación Hardware-in-the-Loop (HIL) en tiempo real, utilizando la arquitectura de doble núcleo del microcontrolador TMS320F28379D de Texas Instruments.

## 🚀 Características del Proyecto

- **Simulación HIL en Tiempo Real:** Ejecución paralela de modelos matemáticos (Planta) y algoritmos de control (PID/PI) en núcleos independientes (CPU1 y CPU2).
- **Diseño Basado en Modelos (MBD):** Integración completa con MATLAB/Simulink y generación automática de código.
- **Casos de Estudio Implementados:**
  - 📍 **Posición Motor DC:** Lazo abierto y Lazo cerrado (PID y sin control).
  - 🏎️ **Velocidad Motor DC:** Control PID ante perturbaciones.
  - 🛢️ **Sistema de Presión:** Control de transferencia de crudo (PI) basado en analogía hidráulico-eléctrica.
- **Validación Experimental:** Comparación de resultados teóricos vs. señales reales adquiridas vía osciloscopio.

## 📂 Estructura del Repositorio

El repositorio está organizado por carpetas según el sistema dinámico a simular. En cada una encontrarás tanto el script de configuración como los modelos de Simulink necesarios:

* `📁 Position`: Control de posición de Motor DC.
    * `Position.mlx`: Script de configuración de parámetros.
    * Archivos `.slx` correspondientes (Control y Planta).
* `📁 Velocity`: Control de velocidad de Motor DC.
    * `Velocity.mlx`: Script de configuración de parámetros.
    * Archivos `.slx` correspondientes (Control y Planta).
* `📁 Pressure`: Sistema de control de presión (Transferencia de crudo).
    * `Configuracion_del_modelo_de_presion.mlx`: Script de configuración de parámetros.
    * Archivos `.slx` correspondientes (Control y Planta).
* `📁 Docs`: Documentación adicional o guía de laboratorio.

## 🛠️ Requisitos de Hardware y Software

### Software
* MATLAB R202x (con Simulink).
* **Toolbox requeridos:**
    * Embedded Coder.
    * C2000 Microcontroller Blockset.
    * MATLAB Coder.

### Hardware
* Tarjeta de desarrollo **TI LaunchPad LAUNCHXL-F28379D**.
* Cables jumper (para cerrar el lazo físico).
* Osciloscopio (opcional, para visualización externa).

## 🔌 Configuración de Conexiones Físicas (Loopback)

Para que el sistema HIL funcione, se debe cerrar el lazo de control físicamente en la tarjeta conectando los pines de los conversores DAC y ADC:

| Señal | Origen (Salida) | Destino (Entrada) | Descripción |
| :--- | :--- | :--- | :--- |
| **Control / SetPoint** | DAC-A (**Pin 30**) | ADC-A (**Pin 25**) | Envío de señal de control o referencia al modelo de la planta (CPU2). |
| **Realimentación** | DAC-B (**Pin 70**) | ADC-B (**Pin 24**) | Retorno de la variable simulada (posición/velocidad/presión) al controlador (CPU1). |

## 🧭 Flujo de Ejecución Recomendado

Para replicar un experimento, dirígete a la carpeta del caso de estudio deseado (ej. `Position`) y sigue estos pasos:

1.  **Carga de Parámetros:**
    Abre y ejecuta el script `.mlx` que se encuentra dentro de la carpeta (ej. `Position.mlx`). Esto cargará en el *Workspace* las variables necesarias (`Kp`, `Ki`, `Kd`, `num`, `den`, tiempos de muestreo, etc.).

2.  **Configuración de Modelos:**
    Abre los archivos de Simulink `.slx` que se encuentran en la misma carpeta (uno para la CPU1 y otro para la CPU2).

3.  **Compilación y Carga:**
    * Asegúrate de que la tarjeta esté conectada vía USB.
    * Desde Simulink, compila y carga el código primero en la **CPU2 (Planta)**.
    * Luego, compila y carga el código en la **CPU1 (Control)**.

4.  **Visualización:**
    * Utiliza las herramientas de *External Mode* de Simulink para ver las señales en tiempo real.
    * Alternativamente, conecta un osciloscopio a los pines **DAC (30 y 70)** para verificar la respuesta física.

## 🧠 Tecnologías Utilizadas

* **MATLAB & Simulink:** Modelado matemático y diseño de controladores.
* **Texas Instruments C2000:** Arquitectura de microcontroladores para tiempo real.
* **Embedded Coder:** Generación de código C/C++ optimizado.

## 📝 Autores

* **Laura Sofia Polania Mendez** - *Ingeniería Electrónica*
* **Cesar Diego Vargas Motta** - *Ingeniería Electrónica*

**Director:** Dr. Fernand Diaz Franco
*Universidad Surcolombiana - Neiva, Colombia*

## 📄 Licencia

Este proyecto se distribuye con fines académicos y educativos.
