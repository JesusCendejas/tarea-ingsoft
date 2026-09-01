# Visión del producto

**Autor:** Jesus Cendejas
**Fecha de la última versión:** 2026-08-20  
**Repositorio:** Alice-IA/airplay-moon-speaker

---

## 1. Descripción del sistema

**Nombre del sistema:** MoonLight

**Descripción:**  
MoonLight es una webapp de control para dispositivos de iluminación inteligente compatibles: lámparas y controladores de tiras LED  MQTT. Desde cualquier navegador, el usuario controla animaciones RGBA en tiempo real, efectos predefinidos, brillo y color, y diseña sus propias animaciones — todo sobre MQTT, sin instalar apps nativas ni depender de un ecosistema cerrado.

**Nota de alcance:** los dispositivos (bocina inteligente, lámparas, controladores de tiras) son productos independientes con su propio firmware. Este proyecto cubre únicamente la webapp; los dispositivos se tratan como sistemas externos que siguen el protocolo MQTT conocido.

---

## 2. Problema y usuarios

**El problema:**  
Las apps para el control de iluminación inteligente están atadas a marcas y ecosistemas propietarios. Quien construye sus propios dispositivos termina sin una interfaz decente: interfaces web básicas que solo funcionan en red local, o código que hay que escribir desde cero para cada dispositivo nuevo.

**Cómo se resuelve hoy sin el sistema:**  
- Usan la app del fabricante y aceptan sus límites.
- Escriben scripts o interfaces web locales por dispositivo, sin reutilizar nada.
- Usan dashboards genéricos (Home Assistant, MQTT Explorer) que no están diseñados para control de iluminación en tiempo real.

**Usuarios del sistema:**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
| Comunidad maker/DIY | Controlar su lámpara, bocina o tira LED sin programar una app desde cero | Que el hardware sea difícil de conseguir o el firmware inestable |
| Consumidor plug-and-play | Que su producto funcione de inmediato | Que le pidan conocimientos técnicos; que la app sea complicada |
| Usuario de otras apps | Control básico y rápido de los dispositivos de la casa sin configurar nada | Agregar una nueva app para controlar mas dispositivos |

**Un conflicto entre usuarios:**  
El usuario casual quiere abrir la web y elegir un efecto/color en dos clics; el maker quiere un editor de animaciones frame a frame. Esa tensión definió la decisión de que los efectos predefinidos sean el flujo principal y el editor de animaciones una capa encima.

---

## 3. Alcance

**Dentro del alcance**

App:
- Conexión con dispositivos vía MQTT over WebSockets, usando la MAC address como identificador.
- Envío de frames de animación RGBA en modo streaming.
- Control de efectos predefinidos: velocidad, intensidad, brillo y paleta de colores.
- Visualización del estado del dispositivo: online/offline, IP, MAC, RSSI, heap libre y versión de firmware.
- Editor de animaciones personalizadas: diseñar secuencias de frames y enviarlas al dispositivo.
- Soporte para múltiples dispositivos: seleccionar a cuál controlar.
- OTA firmware updates (Solo para dispositivos propietarios).

Dispositivo:
- Recepción de audio vía AirPlay (streaming desde iPhone/Mac).
- Recepción de audio vía Bluetooth A2DP.
- Control de tira WS2812 por MQTT: frames RGBA en tiempo real, efectos predefinidos y brillo.
- Web dashboard accesible desde cualquier lugar (MQTT sobre WebSocket público — HiveMQ).
- Configuración WiFi vía captive portal (AP mode).
- Audio output vía I2S.

**Explícitamente fuera del alcance**

- Asistente de voz.
- EQ por hardware.
- EQ por software.
- Multi-room sync: una sola bocina, sin sincronización entre múltiples dispositivos.
- Display/OLED.
- Reproducción de audio en el navegador.
- Configuración de la red WiFi de los dispositivos (cada dispositivo expone su propio captive portal para eso).
- Almacenamiento de animaciones en el navegador (las animaciones se envían y persisten en el dispositivo).
- App móvil nativa: el control es web únicamente.

**In progress**
- Autenticación MQTT: el broker público de desarrollo no tiene auth. Pero la autenticación y ACLs son requisito de la fase de producción.

---

## 4. Tipo de sistema y atributos de calidad

**Tipo de sistema:** Aplicación web de tiempo real para control de dispositivos IoT sobre MQTT. (SAAS)

La arquitectura tiene tres componentes:

1.- **Frontend:** interfaz de control en MQTT.js sobre WebSocket seguro.

2.- **Backend:** gestiona cuentas de usuario, dispositivos registrados y la autorización de qué usuario puede controlar qué dispositivo. También puede persistir animaciones creadas por el usuario y compartirlas entre dispositivos.

3.- **Broker MQTT:** canal de comunicación con los dispositivos. En desarrollo se usa un broker público (HiveMQ, sin autenticación). **En producción se migrará a un broker con autenticación por usuario/dispositivo (ACL por topic)**, de forma que cada usuario solo pueda publicar y suscribirse a los topics de sus propios dispositivos.

**Atributos de calidad prioritarios:**
- *Seguridad:* un usuario solo puede controlar dispositivos que le pertenecen (aislamiento por topic, credenciales únicas por dispositivo).
- *Latencia:* el streaming de frames debe sentirse inmediato (30 fps objetivo de animación).
- *Usabilidad:* activar un efecto debe tomar pocos clics.
- *Portabilidad:* cualquier navegador moderno, desktop o móvil, sin instalación.
- *Interoperabilidad:* cualquier dispositivo que implemente el protocolo MQTT documentado es controlable una vez registrado.
---

## 5. Modelo de desarrollo

**Recomendado:** Iterativo e incremental (Scrum, sprints de 1-2 semanas).

**Por qué encaja:**
- Un solo desarrollador: la ceremonia pesada sobra, pero las iteraciones cortas con demo contra hardware real no.
- Cada sprint entrega un slice vertical usable: conexión → control de efectos → streaming → editor de animaciones.

**Sprints**
- *Sprint 1:* Frontend conectado al broker público y controla efectos y brillo de la Luna ([Ver dispositivo](https://github.com/Alice-IA/airplay-moon-speaker)).
- *Sprint 2:* Streaming de frames RGBA + selección de dispositivo por MAC.
- *Sprint 3:* Backend + DB: cuentas de usuario y registro/vinculación de dispositivos.
- *Sprint 4:* Editor de animaciones personalizadas + persistencia en DB.
- *Sprint 5:* Broker propio con autenticación y ACL por topic; migración del firmware del dispositivo a credenciales.
- *Sprint 6:* Pulido, pruebas y documentación final.

**Alternativa descartada 1:** Cascada. Exige requisitos cerrados al inicio, y en un proyecto que depende de hardware real (latencia MQTT, límites de memoria, comportamiento de los LEDs) los requisitos cambian en la primera prueba.

**Alternativa descartada 2:** Modelo V. La carga documental no se justifica para un solo desarrollador y un sistema sin requisitos de seguridad críticos.

---

