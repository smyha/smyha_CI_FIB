# Descripción de Archivos y Funcionamiento del Sistema

## Archivos

### `config.h`

Este archivo contiene la configuración del PIC, incluyendo las bibliotecas necesarias y definiciones de constantes.

### `animated.h`

Aquí se encuentran las animaciones y funciones de control de la pantalla GLCD. Incluye funciones para animaciones específicas, como el final y generación de barras, así como funciones para dibujar botones y símbolos en la pantalla.

### `main.c`

Este archivo contiene la lógica principal del sistema. Incluye la configuración del PIC, la lógica del temporizador y el manejo de la interfaz de usuario. Define tres estados principales: Ready, Running y Stopped. El usuario puede ajustar el temporizador pulsando los botones, y la animación se inicia cuando ambos botones están presionados simultáneamente.

### `GLCD.h`

Aquí se encuentran las definiciones y funciones relacionadas con la pantalla GLCD. Incluye funciones para inicializar la pantalla, escribir texto y controlar los puntos en la pantalla.

### `ascii.h`

Este archivo contiene la tabla de caracteres ASCII utilizada en el sistema.

## Funcionamiento del Sistema

El sistema opera en tres estados principales:

1. **Ready:** El sistema está listo para recibir la entrada del usuario.
2. **Running:** Se activa cuando ambos botones están presionados simultáneamente. Inicia una animación de barra y decrementa un temporizador.
3. **Stopped:** Indica que el temporizador ha llegado a cero. Muestra un mensaje y finaliza la animación.

El usuario puede ajustar el temporizador pulsando dos botones. Si ambos botones están presionados simultáneamente, se inicia la animación. El temporizador disminuye y muestra el progreso en una barra animada en la pantalla GLCD.


## Funciones Relacionadas con el Temporizador (Timer)

### `void configTMR0()`

Configura el Timer0 del PIC para controlar el temporizador en el sistema. Algunos puntos clave de esta función son:

- Configuración de Timer0 como temporizador de 16 bits.
- Establecimiento del preescalador a 1:32.
- Inicialización del valor de desbordamiento para obtener una interrupción cada 1 segundo.
- Habilitación de la interrupción por desbordamiento del Timer0.

### `void loading_animation()`

Esta función se llama en cada desbordamiento del Timer0 y se encarga de actualizar la animación de la barra de progreso y verificar si se ha alcanzado el final del temporizador. Algunos detalles importantes incluyen:

- Decremento del tamaño de la barra en la pantalla.
- Cambio de estado a "Stopped" cuando el temporizador alcanza cero.
- Reinicio del Timer0 para continuar la cuenta regresiva.

### `void interrupt water_injection_RSI()`

Rutina de servicio de interrupción para el desbordamiento del Timer0. Se ejecuta cada vez que se produce un desbordamiento del temporizador y reinicia la cuenta y la animación.

## Funciones Relacionadas con las Animaciones

### `void endAnimation()`

Esta función realiza una animación al finalizar el temporizador. Borra las barras de progreso de la pantalla en direcciones específicas para dar la apariencia de una animación de cierre.

### `void generateBar()`

Genera la barra de progreso inicial en la pantalla GLCD. Dibuja un contenedor y carga la animación de la barra hasta la mitad.

### `void drawPlus(int x, int y, int radius)`

Dibuja el símbolo "+" en la pantalla GLCD con el centro en las coordenadas (x, y) y el radio especificado.

### `void drawMinus(int x, int y, int radius)`

Dibuja el símbolo "-" en la pantalla GLCD con el centro en las coordenadas (x, y) y el radio especificado.

### `void drawSquare(int x, int y, int size)`

Dibuja un cuadrado en la pantalla GLCD con la esquina superior izquierda en las coordenadas (x, y) y el tamaño especificado.

### `void displayButton()`

Dibuja dos botones en la pantalla GLCD, cada uno con un cuadrado y un símbolo asociado ("+" o "-").

### `void displayPressedButton(int x, int y, int radius)`

Muestra una animación cuando un botón es presionado. Muestra y borra puntos en forma circular alrededor del botón indicando que está siendo presionado.

Estas funciones forman la base del sistema de control de la máquina de café y la interfaz de usuario en la pantalla GLCD. Consulta los comentarios en el código fuente para detalles adicionales y ajustes específicos.
