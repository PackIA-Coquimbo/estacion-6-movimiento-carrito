#include <IRremote.h>

const int PIN_MOTOR = 3;
const int PIN_IR = 2;

bool motorEncendido = false;
unsigned long ultimoTiempo = 0;

void setup() {
  pinMode(PIN_MOTOR, OUTPUT);
  digitalWrite(PIN_MOTOR, LOW); // Motor apagado al inicio

  IrReceiver.begin(PIN_IR); // Inicializar sensor en Pin 2
}

void loop() {
  if (IrReceiver.decode()) {
    // Leemos directamente el comando enviado por el control
    int boton = IrReceiver.decodedIRData.command;

    // Antirrebote de 300 ms
    if (millis() - ultimoTiempo > 300) {
      // Reacciona al Botón 1 (16) o al Botón Rojo (0)
      if (boton == 16 || boton == 0) {
        motorEncendido = !motorEncendido;
        digitalWrite(PIN_MOTOR, motorEncendido ? HIGH : LOW);
        ultimoTiempo = millis();
      }
    }

    IrReceiver.resume(); // Listo para la siguiente pulsación
  }

  delay(10);
}
