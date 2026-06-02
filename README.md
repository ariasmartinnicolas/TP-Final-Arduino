# TP-Final-Arduino
Trabajo Final: Juego de Memoria "Simón Dice" con Máquina de Estados
Materia: Laboratorio de Computación
Universidad Nacional de San Martín (UNSAM)
Plataforma: Arduino Uno (Programado en Lenguaje C)

Integrantes:
Martín Nicolás Arias


1. Descripción del Proyecto
El proyecto consiste en el diseño y desarrollo de un juego de memoria secuencial interactivo basado en la plataforma Arduino Uno. El sistema cuenta con 10 niveles de dificultad fija y progresión lineal, orientados a evaluar la retención visual y auditiva del usuario mediante patrones de luces y sonido que incrementan su complejidad de manera sucesiva.

Dinámica de Funcionamiento:
Fase de Inicialización: Al encender o reiniciar el microcontrolador, el sistema ejecuta de forma automática una secuencia de luces con los LEDs principales acompañada de una melodía de bienvenida.

Generación de Secuencias: El juego comienza en el Nivel 1. El sistema genera un patrón aleatorio cuya longitud está determinada por el nivel actual (desde 1 LED en el Nivel 1 hasta un patrón de 10 LEDs en el Nivel 10). El avance no permite la selección manual de la dificultad; es estrictamente lineal.

Fase de Juego (Espera de Usuario): El usuario debe replicar la secuencia utilizando los cuatro pulsadores del tablero. El sistema procesa estas entradas mediante lógica de flancos para asegurar la precisión de las lecturas físicas.

Condición de Victoria: Si el jugador logra completar de forma correcta el Nivel 10, la pantalla mostrará el mensaje "¡Usted Ganó!" y se reproducirá una melodía de triunfo.

Condición de Fallo (Game Over): Si el usuario presiona un botón incorrecto, el sistema activa de forma inmediata un LED Rojo de error, reproduce una melodía de fallo y despliega en la pantalla el mensaje "Game Over" junto con el puntaje final obtenido.

Sistema de Puntuación:
Puntaje por acierto: Se otorgan +10 puntos por cada botón correcto presionado dentro de la secuencia.

Bono por nivel: Al completar la secuencia entera de un nivel, se suma un adicional multiplicando el nivel alcanzado (ejemplo: +50 puntos en Nivel 1, +100 puntos en Nivel 2, de manera sucesiva).

El puntaje se inicializa en 0 al encender el circuito. Al perder, el puntaje obtenido se mantiene estático en la pantalla como el último registro de la sesión hasta que se inicie una nueva partida.

2. Cumplimiento de Requisitos Mínimos de la Cátedra
Control de Entradas y Salidas (E/S):

Entradas Digitales: 4 pines configurados con resistencias de pulso para registrar las pulsaciones de los 4 botones de juego de manera estable.

Salidas Digitales: 6 pines en modo salida (4 LEDs de colores para la secuencia, 1 LED Verde indicador de acierto/éxito y 1 LED Rojo exclusivo para la indicación visual de error).

Salida Analógica (PWM): Control de frecuencias mediante un Buzzer piezoeléctrico para emitir los tonos correspondientes a cada color y las melodías del sistema.

Entrada Analógica: Lectura de un pin analógico al aire (A0) para obtener ruido electromagnético ambiental, utilizado como semilla aleatoria (randomSeed) para garantizar secuencias diferentes en cada ejecución.

Contador de Flancos:

El software analiza el cambio de estado de los botones comparing el registro actual con el inmediatamente anterior. La acción lógica se ejecuta únicamente al detectar el flanco de bajada (transición de alto a bajo), impidiendo que mantener presionado un pulsador cuente como múltiples respuestas o genere un fallo automático.

Control por Tiempo (Temporizadores):

Se descarta el uso de funciones de espera bloqueantes (delay) durante la fase de juego. Los tiempos de encendido de los LEDs, la duración de los tonos y las ventanas de espera se gestionan utilizando el contador interno del microcontrolador mediante la función no-bloqueante millis().

Máquina de Estados Finita (FSM):

La arquitectura del programa en C se organiza mediante una estructura de selección switch-case basada en 5 estados principales que fragmentan el comportamiento del software de forma modular:

Inicialización / Bienvenida

Generar Secuencia

Espera de Jugador

Nivel Ganado / Victoria Total

Game Over

3. Componentes de Hardware Utilizados
1x Placa Arduino Uno R3

4x LEDs de colores (Azul y Amarillo según diseño físico) para la secuencia de juego

1x LED Verde indicador de nivel superado

1x LED Rojo para indicador de error (Game Over)

4x Pulsadores de presión

1x Buzzer Piezoeléctrico

1x Pantalla LED / Display de texto informativo (para la visualización de niveles y puntajes)

Resistencias de paso para protección de corriente en los LEDs y configuración de pulsadores

1x Protoboard y conductores de conexión
