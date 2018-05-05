# Escanear-Puertos-Arduino

Arduino dispone de soporte I2C por hardware vinculado físicamente a ciertos pines. También es posible emplear cualquier otro grupo de pines como bus I2C a través de software, pero en ese caso la velocidad será mucho menor.

Los pines a los que está asociado varían de un modelo a otro. La siguiente tabla muestra la disposición en alguno de los principales modelos. Para otros modelos, consultar el esquema de patillaje correspondiente.


<table>
<tbody>
<tr>
<td><span style="font-weight:400;">MODELO</span></td>
<td><span style="font-weight:400;">SDA</span></td>
<td><span style="font-weight:400;">SCK</span></td>
</tr>
<tr>
<td><span style="font-weight:400;">Uno</span></td>
<td><span style="font-weight:400;">A4</span></td>
<td><span style="font-weight:400;">A5</span></td>
</tr>
<tr>
<td><span style="font-weight:400;">Yun</span></td>
<td><span style="font-weight:400;">A2</span></td>
<td><span style="font-weight:400;">A3</span></td>
</tr>
<tr>
<td><span style="font-weight:400;">Nano</span></td>
<td><span style="font-weight:400;">A4</span></td>
<td><span style="font-weight:400;">A5</span></td>
</tr>
<tr>
<td><span style="font-weight:400;">Mini Pro</span></td>
<td><span style="font-weight:400;">A4</span></td>
<td><span style="font-weight:400;">A5</span></td>
</tr>
<tr>
<td><span style="font-weight:400;">Mega</span></td>
<td><span style="font-weight:400;">20</span></td>
<td><span style="font-weight:400;">21</span></td>
</tr>

</tbody>

Para usar el bus I2C en Arduino, el IDE Standard proporciona la librería “Wire.h”, que contiene las funciones necesarias para controlar el hardware integrado.

Características de I2C en ATmega328p:

Simple, yet Powerful and Flexible Communication Interface, only two Bus Lines Needed
Both Master and Slave Operation Supported
Device can Operate as Transmitter or Receiver
7-bit Address Space Allows up to 128 Different Slave Addresses
Multi-master Arbitration Support
Up to 400kHz Data Transfer Speed
Slew-rate Limited Output Drivers
Noise Suppression Circuitry Rejects Spikes on Bus Lines
Fully Programmable Slave Address with General Call Support
Address Recognition Causes Wake-up When AVR is in Sleep Mode
Compatible with Philips I2C protocol
La librería para manejar el bus I2C en Arduino es Wire: http://arduino.cc/en/reference/wire

Esta librería permite comunicar con I2C/TWI Arduino con otros dispositivos. En las placas Arduino con el diseño R3 (1.0 pinout), la SDA (línea de datos) y SCL (línea de reloj) están en los pines cerca del pin AREF


<img src="http://javieraliaga.info/arduino/escanerPuertos/ArduinoUno_R3_Pinouts_600.png"/>
</table>

### Funciones:

<ul>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireBegin"><span style="font-weight:400;">begin</span></a><span style="font-weight:400;">() – Inicia la librería Wire y especifica si es master o slave</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireRequestFrom"><span style="font-weight:400;">requestFrom</span></a><span style="font-weight:400;">() – Usado por el maestro para solicitar datos del esclavo</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireBeginTransmission"><span style="font-weight:400;">beginTransmission</span></a><span style="font-weight:400;">() – Comenzar transmisión con esclavo.</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireEndTransmission"><span style="font-weight:400;">endTransmission</span></a><span style="font-weight:400;">() – Finaliza la transmisión que comenzó con un esclavo y transmite los bytes en cola.</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireWrite"><span style="font-weight:400;">write</span></a><span style="font-weight:400;">() – Escribe datos desde un esclavo como respuesta a una petición del maestro o pone en cola la transmisión de un maestro.</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireAvailable"><span style="font-weight:400;">available</span></a><span style="font-weight:400;">() – Devuelve el número de bytes para leer</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireRead"><span style="font-weight:400;">read</span></a><span style="font-weight:400;">() – Lee un byte transmitido desde un esclavo a un maestro o viceversa</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireOnReceive"><span style="font-weight:400;">onReceive</span></a><span style="font-weight:400;">() – Llama a una función cuando un esclavo recibe una transmisión de un maestro. Registra una función de callback.</span></li>
<li style="font-weight:400;"><a href="http://arduino.cc/en/Reference/WireOnRequest"><span style="font-weight:400;">onRequest</span></a><span style="font-weight:400;">() – Llama a una función cuando un maestro solicita datos de un maestro. Registra una función de callback.</span></li>
</ul>

### Escaner I2C
Cada componente que conectamos al bus I2C tiene una dirección única, y cada mensaje y orden que transmitimos al bus, lleva anexa esta dirección, indicando cuál de los muchos posibles, es el receptor del mensaje.

Esto implica que sabemos la dirección del componente. Lo normal es comprobar la información técnica del fabricante del componente, y ahí suele decirnos cuál es la dirección por defecto. Pero es posible que tengamos un dispositivo sin documentación, para ello hay un programa para Arduino, que nos informa, de lo que hay en nuestro bus y con qué dirección.

Ver http://playground.arduino.cc/Main/I2cScanner
