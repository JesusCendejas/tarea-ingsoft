# Visión del producto

**Autor:** Jesus Cendejas
**Fecha de la última versión:** 2026-08-20  
**Repositorio:** Alice-IA/airplay-moon-speaker

---

## 1. Descripción del sistema

**Nombre del sistema:** MoonLight

**Descripción:**  
MoonLight es una app de iluminación para lámparas inteligentes. Es una bocina inteligente personalizable que combina audio inalámbrico (AirPlay y Bluetooth A2DP) con control de luces LED WS2812 por MQTT, todo gestionado desde un dashboard web accesible desde cualquier lugar sin depender de un ecosistema cerrado.

---

## 2. Problema y usuarios

**El problema:**  
Las bocinas y luces inteligentes comerciales encierran al usuario en ecosistemas propietarios, limitan la personalización y obligan a usar múltiples apps para audio e iluminación. Las alternativas DIY existentes suelen quedarse en control local o interfaces web básicas, sin integración remota ni un flujo unificado de audio + luces.

**Cómo se resuelve hoy sin el sistema:**  
- Usan bocinas comerciales cerradas y aceptan las limitaciones del fabricante.  
- Construyen bocinas DIY con control físico (botones) o interfaces web que solo funcionan en red local.  
- Controlan luces y audio por separado (app de luces + app de música).  
- No tienen control remoto de luces desde fuera de casa sin una app nativa.

**Usuarios del sistema:**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
| Comunidad maker/DIY | Una bocina inteligente personalizable, controlable desde web y con código abierto | Que el hardware sea difícil de conseguir o el firmware inestable |
| Integradores de Home Assistant | Audio + luces en un solo dispositivo, controlable programablemente desde su ecosistema | Que la integración con MQTT o Matter sea compleja o poco confiable |
| Usuarios que evitan ecosistemas cerrados | AirPlay + Bluetooth + luces en un solo dispositivo, sin depender de una marca | Que el control remoto dependa de servicios de terceros o autenticación limitada |

**Un conflicto entre usuarios:**  
El integrador de Home Assistant quiere control total programable y eventualmente integración Matter, lo que añade complejidad y consumo de recursos. El usuario maker con un ESP32-S3 de 2 MB PSRAM quiere un firmware ligero y estable. Ese tensionamiento definió la decisión de dejar Matter fuera del alcance inicial y posponerlo al hardware con más PSRAM.

---

## 3. Alcance

**Dentro del alcance**

- Recepción de audio vía AirPlay (streaming desde iPhone/Mac).
- Recepción de audio vía Bluetooth A2DP.
- Control de tira WS2812 por MQTT: frames RGBA en tiempo real, efectos predefinidos y brillo.
- Web dashboard accesible desde cualquier lugar (MQTT sobre WebSocket público — HiveMQ).
- Configuración WiFi vía captive portal (AP mode).
- Reporte de estado del dispositivo vía MQTT (online, IP, MAC, heap libre, RSSI, brillo).
- OTA firmware updates.
- Audio output vía I2S.

**Explícitamente fuera del alcance**

- Asistente de voz.
- EQ por hardware.
- EQ por software.
- Multi-room sync: una sola bocina, sin sincronización entre múltiples dispositivos.
- App móvil nativa: el control es web únicamente (MQTT.js en navegador).
- Autenticación MQTT: el broker público no tiene auth; cualquiera que conozca el MAC del dispositivo puede enviar comandos.
- Display/OLED.

---

## 4. Tipo de sistema y atributos de calidad

**Tipo de sistema:** Sistema embebido IoT con restricciones de tiempo real para audio.

Dispositivo embebido conectado a red que maneja tres flujos concurrentes — audio streaming (AirPlay/Bluetooth), control de LEDs (MQTT), y servicios de red (HTTP server, MQTT client).

---

## 5. Modelo de desarrollo

**Recomendado:** Iterativo e incremental.

**Por qué encaja:**

- Es un solo desarrollador trabajando en hardware + firmware + webapp.
- Los límites de hardware se descubren experimentando, no se saben antes: el PSRAM limitó el buffer de audio, los sockets limitaron AirPlay, el brillo sobrecalentó los LEDs. Cada uno se descubrió en una iteración de prueba-en-hardware.
- El hardware evoluciona (N8R2 → N16R8), y el firmware debe adaptarse cuando llegue el nuevo chip.
- Las features se construyen en slices verticales que funcionan: primero AirPlay, después WebSocket para LEDs, después MQTT, después Matter — cada uno compilable y testeable en hardware real.

**Alternativa descartada 1:** Cascada (Waterfall).