## 1. Cinco cosas que la app hace
- Conecta con dispositivos de iluminación compatibles vía MQTT usando la MAC Address como identificador.
- Envía frames de animación RGBA a los LEDs en modo streaming.
- Ajusta brillo, velocidad y paleta de colores de los efectos de iluminación.
- Muestra el estado e información del dispositivo: online/offline, IP, RSSI, heap libre y versión del firmware.
- Crea animaciones personalizadas diseñando secuencias de frames que se envían al dispositivo.


## 2. Tres cosas que la app no hace
- No reproduce audio desde la app.
- No configura la red WiFi. 
- No almacena animaciones en la web (las envía y es la DB quien las persiste).


## 3. Razón de una exclusión
- **No configura la red WiFi:** cada producto crea su propio access point con un portal web cautivo para configurar el internet - localmente. Ese flujo pertenece al firmware del dispositivo, no a la webapp de control.


## 4. Ideas futuras
- **Music sync:** la app procesa el audio y envía el análisis de frecuencias para sincronizar los LEDs con la música.
- **Animaciones con AI:** el usuario describe una animación en texto o sube una imagen, y la AI genera la animación o la paleta de colores lista para enviar al dispositivo.