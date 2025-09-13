# Modificaciones realizadas para compatibilidad con ESP32-CAM (AI Thinker)

## Cambios aplicados

### 1. Archivo: `http-guardar-sd.cpp`

**Cambios de librerías:**
- ❌ Removido: `#include "SD.h"`
- ❌ Removido: `#define SD_CS 5`
- ✅ Agregado: `#include "SD_MMC.h"`
- ✅ Comentario: `// SD_MMC no requiere pin CS específico para ESP32-CAM`

**Cambios en funciones:**
- `save_face_to_sd()`: Cambio `SD.open()` → `SD_MMC.open()`
- `load_faces_from_sd()`: Cambio `SD.open()` → `SD_MMC.open()`
- `startCameraServer()`: 
  - Cambio `SD.begin(SD_CS)` → `SD_MMC.begin()`
  - Cambio `SD.exists()` → `SD_MMC.exists()`
  - Cambio `SD.mkdir()` → `SD_MMC.mkdir()`

### 2. Archivo: `http-sensor-pir.cpp`

**Estado:** ✅ Ya estaba usando correctamente `SD_MMC.h`
- Usa `#include "SD_MMC.h"`
- Todas las funciones usan `SD_MMC.*` correctamente
- Función `save_image_to_sd()` implementada correctamente

### 3. Archivo: `instrucciones-ssd.md`

**Actualizaciones:**
- ✅ Título actualizado para ESP32-CAM específicamente
- ✅ Explicación del protocolo SD_MMC vs SPI
- ✅ Eliminación de tabla de conexiones (no necesaria para ESP32-CAM)
- ✅ Ejemplo de código actualizado con `SD_MMC.begin()`
- ✅ Tabla comparativa SD vs SD_MMC
- ✅ Notas sobre tarjetas compatibles (32GB máx, FAT32)

### 4. Archivo: `instrucciones-sensor-pir.md`

**Adiciones:**
- ✅ Sección sobre almacenamiento en SD
- ✅ Explicación del uso de librerías `FS.h` y `SD_MMC.h`
- ✅ Información sobre guardado automático en `/sensor-pir/`

## Ventajas de usar SD_MMC en ESP32-CAM

1. **Mayor velocidad**: Protocolo de 4 bits vs SPI de 1 bit
2. **Sin configuración de pines**: Hardware integrado en la placa
3. **Sin pin CS**: No requiere Chip Select
4. **Optimizado**: Diseñado específicamente para ESP32

## Verificación de compatibilidad

✅ **http-guardar-sd.cpp**: Completamente migrado a SD_MMC
✅ **http-sensor-pir.cpp**: Ya usaba SD_MMC correctamente
✅ **Documentación**: Actualizada para ESP32-CAM específicamente

## Pruebas recomendadas

1. Compilar ambos archivos .cpp para verificar que no hay errores
2. Probar con tarjeta microSD formateada en FAT32
3. Verificar creación automática de carpetas `/images/` y `/sensor-pir/`
4. Confirmar guardado de imágenes con nombres únicos

Fecha de modificación: 13 de septiembre de 2025