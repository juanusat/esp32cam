# Instrucciones para conectar y usar tarjeta SD en ESP32

## Conexión de la tarjeta SD al ESP32

Utiliza un módulo lector de tarjeta SD (tipo SPI). Las conexiones típicas son:

| SD Module | ESP32 |
|-----------|-------|
| CS        | GPIO 5 (puedes cambiarlo en el código) |
| MOSI      | GPIO 23 |
| MISO      | GPIO 19 |
| SCK       | GPIO 18 |
| VCC       | 3.3V o 5V |
| GND       | GND |

**Nota:** Verifica que tu módulo SD sea compatible con 3.3V para evitar dañar el ESP32.

## Librerías necesarias en Arduino IDE

1. **SD**
   - Instala la librería oficial de Arduino llamada `SD`.
   - Ve a: Herramientas > Administrar bibliotecas > Busca `SD` y selecciona la de Arduino.

2. **FS**
   - Esta librería viene incluida con el ESP32.

3. **ESP32**
   - Instala el soporte para ESP32 desde: Herramientas > Placa > Gestor de tarjetas > Busca `esp32` y selecciona la oficial de Espressif.

## Pasos adicionales

- Asegúrate de que la carpeta `/images` exista en la SD, o el código la creará automáticamente.
- El pin CS puede cambiar según tu módulo, ajusta la línea `#define SD_CS 5` en el código si usas otro pin.

## Ejemplo de código para inicializar SD

```cpp
#include <FS.h>
#include <SD.h>
#define SD_CS 5

void setup() {
  Serial.begin(115200);
  if (!SD.begin(SD_CS)) {
    Serial.println("No se pudo inicializar la tarjeta SD");
    return;
  }
  Serial.println("SD inicializada correctamente");
}
```

Con esto tendrás la SD lista para guardar y leer imágenes en tu proyecto de reconocimiento facial.
