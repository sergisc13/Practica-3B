´´´#include "BluetoothSerial.h"
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test");
Serial.println("The device started, now you can pair it with bluetooth!");
}
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}
´´´
## Funcionamiento
Comprobamos si el bluetooth esta habilitado
creamos una instancia de BluetoothSerial llamada SerialBT
Después empieza el void setup() , este en la primera línea inicializa una comunicación en serie a una
velocidad de 115200 bauds:
En la siguiente línea inicializa el dispositivo serie Bluetooth y pasa como argumento el nombre del
dispositivo.
Para finalizar creamos el void loop() , en las primeras tres líneas creamos un if, donde verificamos si
se están recibiendo bytes en el puerto serie, si es así que se envíe esa información a través de Bluetooth
al dispositivo conectado.
## SALIDA POR TERMINAL
Se veran mensajes enviados desde otro dispositivo

