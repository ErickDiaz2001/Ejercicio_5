INTRODUCCIÓN

Este informe proporciona una descripción del programa para leer la entrada analógica del canal CH1, el cual está conectado a un divisor resistivo de 2k2 // 2k2. 
El programa imprime el valor de la lectura a través de la interfaz UART, mostrando tanto el valor leído como el valor máximo posible de la lectura (4096).

CONFIGURACIÓN 

El system clock del microcontrolador se configuro a 72Mhz.
Se utilizará el ADC1, habilitando continuous conversión mode, con un tiempo de muestreo de 239.5 ciclos, además de habilitar la interrupción. 
Para la comunicación se utilizó el USART3, sin interrupcion.

![image](https://github.com/ErickDiaz2001/Ejercicio_5/assets/169405943/c62b9a8a-4a09-4445-ba99-96601eccae13)

FUNCIONAMIENTO DEL DIVISOR RESISTIVO

El divisor resistivo de 2k2 // 2k2 divide la tensión de entrada a la mitad. Esto significa que si la tensión de entrada es de 3.3V, la tensión en el pin del ADC será de 1.65V.
El ADC del microcontrolador convierte esta tensión en un valor digital de aproximadamente de 2048.

![image](https://github.com/ErickDiaz2001/Ejercicio_5/assets/169405943/559ea9d5-122d-426c-9a3b-de69e5ff8b41)

![image](https://github.com/ErickDiaz2001/Ejercicio_5/assets/169405943/9458e222-8d0c-4a42-800c-6edcc341c471)

EXPLICACIÓN DEL CÓDIGO

1.	INCLUSIÓN DE BIBLIOTECAS:

o	stdio.h: contiene las definiciones y funciones básicas que nos permite realizar operaciones de entrada y salida en C, como printf() y scanf().

o	itoa.h: convierte el número entero n en una cadena de caracteres.

LECTURA DEL VALOR DEL ADC:

	Se utiliza la función HAL_ADC_GetValue() para leer el valor del ADC.

o	CÁLCULO DEL VOLTAJE REAL:

	Se calcula el voltaje real utilizando la siguiente fórmula: Voltaje = (adc_Valor * Voltaje de referencia) / (2^Resolución)

	La fórmula toma en cuenta el valor leído del ADC (2071 a 2085), la tensión de referencia del ADC (3.3V) y la resolución del ADC(12 bit = 4096).

o	IMPRESIÓN DEL RESULTADO:

	Se utiliza la función printf() para imprimir en la UART el valor leído del ADC ("ADC CH1 value: ") seguido del valor leído, luego se imprimir el mensaje "Max sample value: " seguido del valor máximo posible de la lectura (4096).

	Otra opción es de utilizar la función itoa() para la conversión de los valores e imprimirlo mediante hal_uart_transmit().

ANÁLISIS DE RESULTADOS 

![image](https://github.com/ErickDiaz2001/Ejercicio_5/assets/169405943/9f733e73-0b6f-4197-a62d-abaac3edb565)


CONCLUSIÓN

Este informe describe un programa para leer la entrada analógica del canal CH1, el cual está conectado a un divisor resistivo de 2k2 // 2k2. 
El programa imprime el valor de la lectura a través de la interfaz UART, mostrando tanto el valor digital leído del ADC como el valor máximo posible de la lectura (2048).

El programa es simple, eficiente y permite la adquisición de datos de sensores analógicos conectados a un divisor resistivo. 
Para mejorar la precisión y robustez del sistema, se pueden implementar consideraciones futuras como filtros para suavizar las lecturas del ADC y procedimientos de calibración
para ajustar la exactitud de las mediciones.
