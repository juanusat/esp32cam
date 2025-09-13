# Instrucciones para conectar y usar tarjeta SD en ESP32-CAM (AI Thinker)

## Conexión de la tarjeta SD en ESP32-CAM

La placa AI Thinker ESP32-CAM tiene un slot para tarjeta microSD incorporado que utiliza el protocolo SD_MMC (4-bit). No necesitas conectar cables adicionales, simplemente inserta la tarjeta microSD en el slot.

**Ventajas del protocolo SD_MMC:**
- Mayor velocidad de transferencia que SPI
- No requiere pines CS (Chip Select)
- Conexión directa al controlador MMC del ESP32
- Conexiones de hardware ya configuradas en la placa

## Librerías necesarias en Arduino IDE

1. **SD_MMC**
   - Librería integrada en el framework ESP32
   - Compatible con el protocolo SD_MMC de 4 bits
   - Optimizada para ESP32-CAM

2. **FS**
   - Esta librería viene incluida con el ESP32
   - Sistema de archivos base

3. **ESP32**
   - Instala el soporte para ESP32 desde: Herramientas > Placa > Gestor de tarjetas > Busca `esp32` y selecciona la oficial de Espressif

## Pasos adicionales

- Asegúrate de que la carpeta `/images` exista en la SD, o el código la creará automáticamente
- Usa tarjetas microSD de hasta 32GB (formato FAT32)
- La tarjeta debe estar formateada en FAT32 para mejor compatibilidad
- No se requiere configuración de pines adicionales

## Ejemplo de código para inicializar SD_MMC

```cpp
#include "FS.h"
#include "SD_MMC.h"

void setup() {
  Serial.begin(115200);
  
  // Inicializar SD_MMC (sin parámetros para modo 4-bit)
  if (!SD_MMC.begin()) {
    Serial.println("No se pudo inicializar la tarjeta SD");
    return;
  }
  
  Serial.println("SD inicializada correctamente");
  
  // Crear carpeta si no existe
  if (!SD_MMC.exists("/images")) {
    SD_MMC.mkdir("/images");
    Serial.println("Carpeta /images creada");
  }
}
```

## Diferencias principales con la librería SD tradicional

| Característica | SD (SPI) | SD_MMC |
|----------------|----------|---------|
| Velocidad | Más lenta | Más rápida |
| Pines requeridos | CS, MOSI, MISO, SCK | Integrados en ESP32-CAM |
| Configuración | Manual | Automática |
| Protocolo | SPI | SD_MMC 4-bit |
| Función de inicio | `SD.begin(CS_PIN)` | `SD_MMC.begin()` |

Con esto tendrás la SD lista para guardar y leer imágenes en tu proyecto de reconocimiento facial.
