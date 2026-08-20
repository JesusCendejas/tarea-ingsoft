nombre: MoonLight

Mi sistema es una app de iluminacion para lamparas inteligentes. 

Descripción
MoonLight: App para control de luces inteligentes wifi.

Problema y usuarios

A quién le sirve:
Comunidad maker/DIY que quiere una bocina inteligente personalizable
Personas que integran audio y luces en Home Assistant y quieren control programable
Quienes quieren AirPlay + Bluetooth + luces en un solo dispositivo sin depender de un ecosistema cerrado

Qué hacen hoy sin el sistema:
Usan bocinas comerciales cerradas y aceptan las limitaciones del fabricante
Construyen bocinas DIY con control físico (botones) o web interfaces que solo funcionan en red local
Controlan luces y audio por separado (app de luces + app de música)
No tienen control remoto de luces desde fuera de casa sin una app nativa

Alcance

Incluye:
Recepción de audio via AirPlay (streaming desde iPhone/Mac)
Recepción de audio via Bluetooth A2DP
Control de tira WS2812 por MQTT: frames RGBA en tiempo real, efectos predefinidos, brillo
Web dashboard accesible desde cualquier lugar (MQTT sobre WebSocket público — HiveMQ)
Configuración WiFi via captive portal (AP mode)
Reporte de estado del dispositivo via MQTT (online, IP, MAC, heap libre, RSSI, brillo)
OTA firmware updates
Audio output via I2S 

Queda fuera:
Asistente de voz
EQ por hardware
EQ por software
Multi-room sync — una sola bocina, sin sincronización entre múltiples dispositivos
App móvil nativa — el control es web únicamente (MQTT.js en navegador)
Autenticación MQTT — el broker público no tiene auth; cualquiera que conozca el MAC del dispositivo puede enviar comandos
Display/OLED

Tipo de sistema y atributos de calidad

Tipo: Sistema embebido IoT con restricciones de tiempo real para audio.

Dispositivo embebido conectado a red que maneja tres flujos concurrentes — audio streaming (AirPlay/Bluetooth), control de LEDs (MQTT), y servicios de red (HTTP server, MQTT client).

Modelo de desarrollo
Recomendado: Iterativo e incremental
Por qué encaja:
Es un solo desarrollador (tú) trabajando en hardware + firmware + webapp
Los límites de hardware se descubren experimentando, no se saben antes — el PSRAM limitó el buffer de audio, los sockets limitaron AirPlay, el brillo sobrecalentó los LEDs. Cada uno se descubrió en una iteración de prueba-en-hardware.
El hardware evoluciona (N8R2 → N16R8), y el firmware debe adaptarse cuando llegue el nuevo chip
Las features se construyen en slices verticales que funcionan: primero AirPlay, después WebSocket para LEDs, después MQTT, después Matter — cada uno compilable y testeable en hardware real
Alternativa descartada 1: Cascada (Waterfall)



