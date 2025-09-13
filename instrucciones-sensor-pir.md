# Instrucciones para conectar el sensor PIR al ESP32-CAM

1. **Identifica los pines del sensor PIR:**
   - VCC: alimentación (normalmente 5V o 3.3V)
   - GND: tierra
   - OUT: señal de salida (detecta movimiento)

2. **Conexión al ESP32-CAM:**
   - Conecta el pin VCC del PIR al pin 3.3V del ESP32-CAM.
   - Conecta el pin GND del PIR al pin GND del ESP32-CAM.
   - Conecta el pin OUT del PIR a un pin GPIO digital del ESP32-CAM (por ejemplo, GPIO13).

3. **Configuración recomendada:**
   - Usa cables cortos para evitar interferencias.
   - Si el sensor PIR tiene un jumper de voltaje, selecciona 3.3V.
   - Puedes ajustar la sensibilidad y el tiempo de retardo del PIR usando los potenciómetros del módulo.

4. **Ejemplo de conexión:**
   - PIR VCC → ESP32-CAM 3.3V
   - PIR GND → ESP32-CAM GND
   - PIR OUT → ESP32-CAM GPIO13

5. **Verifica la conexión:**
   - Antes de alimentar el ESP32-CAM, revisa que las conexiones sean correctas para evitar daños.

6. **Notas adicionales:**
   - El sensor PIR puede tardar unos segundos en estabilizarse tras encenderse.
   - Si usas otro pin GPIO, actualiza el código en consecuencia.

7. **Almacenamiento en SD (ESP32-CAM):**
   - El código utiliza las librerías `FS.h` y `SD_MMC.h` para guardar imágenes cuando se detecta movimiento.
   - La tarjeta microSD se inserta directamente en el slot de la ESP32-CAM.
   - Las imágenes se guardan automáticamente en la carpeta `/sensor-pir/` con nombres únicos basados en timestamp.
