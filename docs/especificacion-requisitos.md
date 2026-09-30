# Especificación de requisitos

**Plantilla del curso · Ingeniería de Software I · SIS3407**

| Campo | Valor |
|---|---|
| **Sistema** | MoonLight |
| **Autor** | Jesus Cendejas |
| **Versión** | 1.0 |
| **Fecha de la última actualización** | 2026-09-29 |



## 1. Propósito y alcance

**Propósito del documento:**
Este documento especifica los requisitos funcionales y no funcionales de MoonLight, los casos de uso que los realizan y la trazabilidad entre requisitos, casos de uso y prototipo. Es la referencia para el diseño del sistema, la revisión de la dupla y la validación del prototipo de la semana 8. Va dirigido al desarrollador, a la dupla revisora y al docente del curso.

**Alcance del sistema:**
MoonLight es una progressive web app (PWA) de control para dispositivos de iluminación inteligente compatibles con el protocolo MQTT documentado: lámparas, bocinas con luces y controladores de tiras LED. El usuario controla animaciones RGBA en tiempo real, efectos predefinidos (velocidad, intensidad, brillo, paleta de colores), consulta el estado de sus dispositivos, diseña animaciones personalizadas frame a frame y las reutiliza en cualquiera de sus dispositivos. El sistema gestiona cuentas de usuario, la vinculación de dispositivos por su identificador único (MAC) y actualizaciones de firmware OTA para dispositivos propietarios. Este alcance se retoma de la Visión del producto.

**Fuera del alcance:**
- La configuración de la red WiFi de los dispositivos: cada dispositivo expone su propio captive portal.
- El almacenamiento de animaciones en el navegador: las animaciones se envían al dispositivo y persisten allí (y en la cuenta del usuario vía backend).
- Las apps móviles nativas: el control es web únicamente.
- El firmware de los dispositivos: son productos independientes que se tratan como sistemas externos que siguen el protocolo MQTT conocido.



## 2. Usuarios y su contexto

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
|---|---|---|
| Comunidad maker/DIY | Escribe scripts o interfaces web locales por dispositivo, sin reutilizar nada; o usa dashboards genéricos (Home Assistant, MQTT Explorer) que no están diseñados para control de iluminación en tiempo real | Controlar su lámpara, bocina o tira LED sin programar una app desde cero; un editor de animaciones frame a frame; que el protocolo sea abierto y cualquier dispositivo compatible se pueda vincular |
| Consumidor plug-and-play | Usa la app del fabricante y acepta sus límites; o descarta el producto si le exige conocimientos técnicos | Que su dispositivo funcione de inmediato: elegir un efecto o color en pocos toques, sin registrar nada técnico |

**Conflictos identificados entre usuarios:**
El usuario casual quiere abrir la web y elegir un efecto o color en dos clics; el maker quiere un editor de animaciones frame a frame. Resolución adoptada: los efectos predefinidos son el flujo principal de la app y el editor de animaciones es una capa encima, no un requisito bloqueante del flujo principal.



## 3. Requisitos funcionales

### 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
|---|---|---|---|
| RF-001 | Registro de cuenta | Imprescindible | Visión del producto |
| RF-002 | Vincular un dispositivo por MAC | Imprescindible | Visión del producto |
| RF-003 | Una MAC, una sola cuenta | Imprescindible | Visión del producto |
| RF-004 | Lista de dispositivos con estado | Imprescindible | Visión del producto |
| RF-005 | Detección de desconexión | Imprescindible | Visión del producto |
| RF-006 | Estado detallado del dispositivo | Importante | Visión del producto |
| RF-007 | Activar un efecto predefinido | Imprescindible | Conflicto de usuarios (flujo principal) |
| RF-008 | Ajustar el brillo | Imprescindible | Visión del producto |
| RF-009 | Detener el efecto o animación | Imprescindible | Visión del producto |
| RF-010 | Transmitir frames RGBA en streaming | Imprescindible | Visión del producto |
| RF-011 | El último comando gana | Imprescindible | Protocolo del dispositivo (docs/API.md) |
| RF-012 | Bloquear comandos a dispositivos desconectados | Importante | Caso de uso CU-04 (flujo alterno) |
| RF-013 | Crear una animación personalizada | Importante | Conflicto de usuarios (capa maker) |
| RF-014 | Guardar animaciones en la cuenta | Importante | Visión del producto |
| RF-015 | Enviar animación guardada a cualquier dispositivo | Importante | Visión del producto |
| RF-016 | Actualización OTA para dispositivos propietarios | Deseable | Visión del producto |
| RF-017 | Iniciar sesión | Imprescindible | Caso de uso CU-02 |
| RF-018 | Editar el nombre de un dispositivo | Importante | Caso de uso CU-05 |
| RF-019 | Consultar escenas | Importante | Caso de uso CU-11 |
| RF-020 | Guardar una escena multi-dispositivo | Importante | Caso de uso CU-12 |
| RF-021 | Aplicar una escena | Importante | Caso de uso CU-11, CU-12 |
| RF-022 | Guardar colores favoritos | Importante | Caso de uso CU-13 |
| RF-023 | Registrar una habitación | Importante | Caso de uso CU-15 |
| RF-024 | Asignar un dispositivo a una habitación | Importante | Caso de uso CU-16 |
| RF-025 | Agrupar escenas por habitación | Deseable | Decisión de diseño: organización por ubicación |

### 3.2 Fichas

**RF-001 · Registro de cuenta**

| Campo | Contenido |
|---|---|
| Descripción | El sistema registra una cuenta de usuario nueva con correo y contraseña, e inicia la sesión tras el registro. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al registrar un correo no existente y una contraseña válida, la cuenta queda creada y el usuario queda con la sesión iniciada, sin dispositivos vinculados. Si el correo ya está registrado, el sistema no crea nada, avisa y ofrece iniciar sesión. |
| Relacionado con | RF-002, RNF-SEG-001, RNF-USA-002 |

**RF-002 · Vincular un dispositivo por MAC**

| Campo | Contenido |
|---|---|
| Descripción | El sistema vincula un dispositivo a la cuenta del usuario usando la dirección MAC como identificador único, y lo muestra en su lista de dispositivos. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al ingresar una MAC válida (12 caracteres hexadecimales), el dispositivo queda vinculado a la cuenta y aparece en la lista con su estado. Si el dispositivo no responde en ese momento, se vincula igual pero queda marcado como desconectado. |
| Relacionado con | RF-001, RF-003, RF-004, RNF-INT-001 |

**RF-003 · Una MAC, una sola cuenta**

| Campo | Contenido |
|---|---|
| Descripción | El sistema impide vincular una misma dirección MAC a dos cuentas distintas. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al intentar vincular una MAC ya vinculada a otra cuenta, el sistema rechaza el registro y avisa al usuario; la cuenta original no se ve afectada. |
| Relacionado con | RF-002, RNF-SEG-001 |

**RF-004 · Lista de dispositivos con estado**

| Campo | Contenido |
|---|---|
| Descripción | El sistema muestra la lista de dispositivos vinculados al usuario, cada uno con su estado: conectado o desconectado. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | La lista muestra todos los dispositivos vinculados a la cuenta y ninguno más; cada uno muestra un estado que corresponde a si está reportando o no en ese momento. |
| Relacionado con | RF-002, RF-005, RNF-REN-003 |

**RF-005 · Detección de desconexión**

| Campo | Contenido |
|---|---|
| Descripción | El sistema marca como desconectado cualquier dispositivo que deje de reportar su estado. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Un dispositivo que deja de reportar pasa a mostrarse como desconectado en la interfaz dentro del plazo definido en RNF-REN-003. Un dispositivo que vuelve a reportar pasa a conectado sin recargar la página. |
| Relacionado con | RF-004, RF-012, RNF-REN-003 |

**RF-006 · Estado detallado del dispositivo**

| Campo | Contenido |
|---|---|
| Descripción | El sistema muestra el estado detallado del dispositivo seleccionado: IP, MAC, señal WiFi (RSSI), memoria libre y versión de firmware. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Importante |
| Criterio de aceptación | Al seleccionar un dispositivo conectado, la pantalla muestra los cinco datos reportados por el propio dispositivo. Los datos corresponden al último estado reportado, no a valores en caché de una sesión anterior. |
| Relacionado con | RF-004, RF-016, RNF-REN-003 |

**RF-007 · Activar un efecto predefinido**

| Campo | Contenido |
|---|---|
| Descripción | El sistema envía al dispositivo seleccionado un efecto predefinido con sus parámetros: velocidad, intensidad, brillo y paleta de colores. |
| Origen | Conflicto de usuarios: el flujo principal del consumidor casual debe tomar pocos toques. Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al elegir un efecto (con o sin ajustar parámetros), el dispositivo lo reproduce de inmediato con los parámetros indicados. Si había una animación en curso, el efecto la reemplaza. |
| Relacionado con | RF-008, RF-011, RF-012, RNF-USA-001, RNF-REN-002 |

**RF-008 · Ajustar el brillo**

| Campo | Contenido |
|---|---|
| Descripción | El sistema ajusta el brillo del dispositivo en un rango de 0 a 255. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al fijar un valor entre 0 y 255, el brillo del dispositivo cambia al valor indicado. Valores fuera del rango no se envían. |
| Relacionado con | RF-007, RNF-REN-002 |

**RF-009 · Detener el efecto o animación**

| Campo | Contenido |
|---|---|
| Descripción | El sistema detiene el efecto o animación en curso cuando el usuario lo indica. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al tocar "Detener" en un dispositivo que reproduce algo, las luces se apagan. Si el dispositivo está desconectado, el sistema no envía la orden y avisa. |
| Relacionado con | RF-012 |

**RF-010 · Transmitir frames RGBA en streaming**

| Campo | Contenido |
|---|---|
| Descripción | El sistema envía frames de animación RGBA en modo streaming al dispositivo seleccionado, en tiempo real. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Al entrar al modo streaming y generar frames, el dispositivo los reproduce a la tasa definida en RNF-REN-001. Al salir del modo streaming, el canal se cierra y el dispositivo queda listo para el siguiente comando. |
| Relacionado con | RF-011, RNF-REN-001, RNF-REN-002 |

**RF-011 · El último comando gana**

| Campo | Contenido |
|---|---|
| Descripción | Cuando un efecto y un streaming se envían sobre el mismo dispositivo, el sistema ejecuta el último comando recibido. |
| Origen | Protocolo del dispositivo (docs/API.md): comportamiento confirmado del firmware. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Con una animación en curso, enviar un efecto lo reemplaza; con un efecto en curso, iniciar un streaming lo reemplaza. En todo momento el dispositivo reproduce solo el último comando recibido. |
| Relacionado con | RF-007, RF-009, RF-010 |

**RF-012 · Bloquear comandos a dispositivos desconectados**

| Campo | Contenido |
|---|---|
| Descripción | El sistema impide enviar comandos a un dispositivo marcado como desconectado y avisa al usuario. |
| Origen | Caso de uso CU-04, flujo alterno 4a. Confirmado por el cliente. |
| Prioridad | Importante |
| Criterio de aceptación | Con el dispositivo marcado como desconectado, cualquier comando (efecto, brillo, detención, streaming, animación guardada) se bloquea en la interfaz y el usuario recibe un aviso; el dispositivo no recibe nada. |
| Relacionado con | RF-005, RF-007, RF-009 |

**RF-013 · Crear una animación personalizada**

| Campo | Contenido |
|---|---|
| Descripción | El sistema permite diseñar una animación personalizada como secuencia de frames, definiendo el color de cada LED y la duración de cada frame. |
| Origen | Conflicto de usuarios: capa maker sobre el flujo principal. Confirmado por el cliente. |
| Prioridad | Importante |
| Criterio de aceptación | El editor muestra la cuadrícula de LEDs del dispositivo y la línea de tiempo de frames; el usuario puede fijar el color de cada LED por frame y la duración de cada frame, y probar la animación en el dispositivo antes de guardarla. |
| Relacionado con | RF-010, RF-014 |

**RF-014 · Guardar animaciones en la cuenta**

| Campo | Contenido |
|---|---|
| Descripción | El sistema guarda las animaciones personalizadas en la cuenta del usuario. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Importante |
| Criterio de aceptación | Una animación guardada con nombre queda disponible en la biblioteca de la cuenta tras cerrar y volver a abrir la sesión. Las animaciones no se almacenan en el navegador. |
| Relacionado con | RF-013, RF-015 |

**RF-015 · Enviar animación guardada a cualquier dispositivo**

| Campo | Contenido |
|---|---|
| Descripción | El sistema permite enviar una animación guardada a cualquier dispositivo vinculado a la cuenta, aunque no sea el dispositivo donde se creó. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Importante |
| Criterio de aceptación | Una animación creada para un dispositivo se envía a otro dispositivo vinculado con distinta cantidad de LEDs y se reproduce adaptada a esa cantidad. El dispositivo destino conserva la animación aunque el usuario cierre la página. |
| Relacionado con | RF-014, RF-012, RNF-INT-001 |

**RF-016 · Actualización OTA para dispositivos propietarios**

| Campo | Contenido |
|---|---|
| Descripción | El sistema ofrece actualizaciones de firmware OTA únicamente para dispositivos propietarios. |
| Origen | Visión del producto (2026-09-01). Confirmado por el cliente. |
| Prioridad | Deseable |
| Criterio de aceptación | Para un dispositivo propietario con versión nueva disponible, el usuario confirma la actualización, el dispositivo se reinicia con la versión nueva y el sistema muestra la versión actualizada. Para un dispositivo no propietario, la opción no se ofrece. Si la actualización falla, el dispositivo conserva su versión anterior y el sistema lo reporta. |
| Relacionado con | RF-006 |



**RF-017 · Iniciar sesión**

| Campo | Contenido |
|---|---|
| Descripción | El sistema autentica al usuario con su correo y contraseña y abre su sesión. |
| Origen | Caso de uso CU-02. El flujo de sesión es previo a todo uso de la cuenta. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Con credenciales correctas, el usuario entra a su cuenta y ve su lista de dispositivos. Con credenciales incorrectas, el sistema avisa y no abre la sesión. |
| Relacionado con | RF-001 |

**RF-018 · Editar el nombre de un dispositivo**

| Campo | Contenido |
|---|---|
| Descripción | El sistema permite editar el nombre de un dispositivo vinculado. |
| Origen | Caso de uso CU-05. Necesidad del cliente con varios dispositivos del mismo modelo. |
| Prioridad | Importante |
| Criterio de aceptación | Tras editar y confirmar, el nombre nuevo aparece en la lista de dispositivos y persiste al cerrar sesión. El sistema rechaza nombres vacíos. |
| Relacionado con | RF-004, RF-024 |

**RF-019 · Consultar escenas**

| Campo | Contenido |
|---|---|
| Descripción | El sistema muestra las escenas guardadas en la cuenta del usuario, cada una con los dispositivos que incluye. |
| Origen | Caso de uso CU-11. Necesidad del cliente: reactivar configuraciones en un toque. |
| Prioridad | Importante |
| Criterio de aceptación | La sección de escenas muestra todas las escenas de la cuenta con sus dispositivos incluidos; una cuenta sin escenas muestra una guía para crear la primera. |
| Relacionado con | RF-020, RF-021, RF-025 |

**RF-020 · Guardar una escena multi-dispositivo**

| Campo | Contenido |
|---|---|
| Descripción | El sistema guarda una escena con la configuración de varios dispositivos (efecto, animación, color, brillo) para activarla en conjunto. |
| Origen | Caso de uso CU-12. Necesidad del cliente: la luna y la lámpara encendidas juntas. |
| Prioridad | Importante |
| Criterio de aceptación | Una escena guardada con nombre incluye al menos un dispositivo con su configuración y queda disponible tras cerrar y reabrir la sesión. |
| Relacionado con | RF-019, RF-021 |

**RF-021 · Aplicar una escena**

| Campo | Contenido |
|---|---|
| Descripción | El sistema aplica una escena enviando a cada dispositivo incluido su configuración guardada. |
| Origen | Caso de uso CU-11, flujo principal. |
| Prioridad | Importante |
| Criterio de aceptación | Al activar una escena, cada dispositivo disponible reproduce su configuración guardada; los dispositivos desconectados se omiten y se reportan. |
| Relacionado con | RF-019, RF-012 |

**RF-022 · Guardar colores favoritos**

| Campo | Contenido |
|---|---|
| Descripción | El sistema guarda colores favoritos en la cuenta del usuario, disponibles en el selector de color de todos sus dispositivos. |
| Origen | Caso de uso CU-13. Uso repetido de los mismos colores. |
| Prioridad | Importante |
| Criterio de aceptación | Un color agregado a favoritos aparece en el selector de color de todos los dispositivos de la cuenta y persiste tras cerrar sesión. El sistema no duplica colores existentes. |
| Relacionado con | RF-007, RF-008 |

**RF-023 · Registrar una habitación**

| Campo | Contenido |
|---|---|
| Descripción | El sistema registra habitaciones en la cuenta del usuario para organizar sus dispositivos y escenas por ubicación. |
| Origen | Caso de uso CU-15. Decisión de diseño: organización por habitación. |
| Prioridad | Importante |
| Criterio de aceptación | Una habitación creada con nombre aparece en la lista de habitaciones de la cuenta; el sistema rechaza nombres vacíos y no duplica habitaciones con el mismo nombre. |
| Relacionado con | RF-024, RF-025 |

**RF-024 · Asignar un dispositivo a una habitación**

| Campo | Contenido |
|---|---|
| Descripción | El sistema asigna un dispositivo a una habitación y lo muestra agrupado por ubicación en la lista de dispositivos. |
| Origen | Caso de uso CU-16. Decisión de diseño: organización por habitación. |
| Prioridad | Importante |
| Criterio de aceptación | Tras asignar una habitación, el dispositivo aparece agrupado bajo esa habitación en la lista; la asignación persiste tras cerrar sesión. |
| Relacionado con | RF-004, RF-023 |

**RF-025 · Agrupar escenas por habitación**

| Campo | Contenido |
|---|---|
| Descripción | El sistema agrupa las escenas de la cuenta por habitación. |
| Origen | Decisión de diseño: organización por habitación (2026-09-30). |
| Prioridad | Deseable |
| Criterio de aceptación | Las escenas se muestran agrupadas por la habitación de los dispositivos que incluyen; una escena multi-habitación aparece en cada habitación incluida. |
| Relacionado con | RF-019, RF-023 |

## 4. Requisitos no funcionales

### 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
|---|---|---|---|---|
| RNF-REN-001 | Rendimiento | Streaming a 30 fps | Imprescindible | Tipo de sistema: control en tiempo real |
| RNF-REN-002 | Rendimiento | Latencia de control < 500 ms | Imprescindible | Tipo de sistema: control en tiempo real |
| RNF-REN-003 | Rendimiento | Cambio de estado visible < 30 s | Imprescindible | Atributo de calidad: usabilidad del estado |
| RNF-SEG-001 | Seguridad | Aislamiento por topic | Imprescindible (fase de producción, Sprint 5) | Atributo de calidad: seguridad |
| RNF-SEG-002 | Seguridad | Credenciales únicas por dispositivo | Imprescindible (fase de producción, Sprint 5) | Atributo de calidad: seguridad |
| RNF-USA-001 | Usabilidad | Efecto en máximo 3 toques | Imprescindible | Conflicto de usuarios: flujo casual |
| RNF-USA-002 | Usabilidad | Primer efecto en < 5 minutos | Importante | Conflicto de usuarios: flujo casual |
| RNF-POR-001 | Portabilidad | Navegadores modernos sin instalación | Imprescindible | Tipo de sistema: PWA |
| RNF-INT-001 | Interoperabilidad | Dispositivo nuevo sin modificar el sistema | Imprescindible | Tipo de sistema: protocolo abierto |

### 4.2 Fichas

**Rendimiento**

**RNF-REN-001 · Streaming a 30 fps**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Rendimiento |
| Descripción | El streaming de animación sostiene 30 frames por segundo sin saltos visibles con el dispositivo en la misma red que el broker. |
| Métrica | Frames por segundo efectivos medidos en el dispositivo durante un streaming de 60 segundos; se acepta la pérdida de frames atrasados, no saltos visibles en la reproducción. |
| Origen | Derivado del tipo de sistema: control de iluminación en tiempo real; objetivo de animación definido en la Visión del producto. |
| Prioridad | Imprescindible |
| Por qué importa | Un streaming con saltos se percibe como una animación rota, no como lentitud: el usuario abandona el modo streaming y vuelve a los efectos predefinidos. |
| Afecta a | RF-010, RF-013 |

**RNF-REN-002 · Latencia de control < 500 ms**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Rendimiento |
| Descripción | El tiempo entre que el usuario toca un control y el dispositivo reacciona es menor a 500 ms con conexión a internet normal. |
| Métrica | Tiempo entre el toque en la interfaz y el cambio observable en el dispositivo, medido con ping < 100 ms hacia el broker; promedio de 10 mediciones por control. |
| Origen | Derivado del tipo de sistema: control interactivo de iluminación. |
| Prioridad | Imprescindible |
| Por qué importa | El control de luces es un acto visual: si el dispositivo no reacciona casi de inmediato, el usuario repite el comando y genera duplicados. |
| Afecta a | RF-007, RF-008, RF-009 |

**RNF-REN-003 · Cambio de estado visible < 30 s**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Rendimiento |
| Descripción | Un cambio de estado del dispositivo (conectado ↔ desconectado) se refleja en la interfaz en menos de 30 segundos. |
| Métrica | Tiempo entre la desconexión (o reconexión) real del dispositivo y el cambio del indicador en la interfaz, sin recargar la página. |
| Origen | Derivado de la cadencia de reporte de estado del protocolo del dispositivo (publicación cada 30 s con mensaje de última voluntad). |
| Prioridad | Imprescindible |
| Por qué importa | El estado desactualizado hace que el usuario envíe comandos a un dispositivo apagado y crea que la app falló. |
| Afecta a | RF-005, RF-012 |

**Seguridad**

**RNF-SEG-001 · Aislamiento por topic**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Seguridad |
| Descripción | Un usuario solo puede publicar y suscribirse a los topics MQTT de sus propios dispositivos; cualquier intento sobre un topic ajeno es rechazado por el broker. |
| Métrica | Con dos cuentas de prueba y un dispositivo vinculado a cada una, el 100 % de las publicaciones y suscripciones hacia el topic del dispositivo ajeno son rechazadas por el broker. |
| Origen | Atributo de calidad declarado en la Visión del producto. Fase de producción: Sprint 5 (el broker público de desarrollo no tiene autenticación). |
| Prioridad | Imprescindible (fase de producción) |
| Por qué importa | Sin aislamiento, cualquiera que conozca una MAC puede controlar las luces de otro usuario; el registro de dispositivos perdería sentido. |
| Afecta a | RF-002, RF-003 |

**RNF-SEG-002 · Credenciales únicas por dispositivo**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Seguridad |
| Descripción | Cada dispositivo usa credenciales MQTT únicas, distintas de las de cualquier otro dispositivo. |
| Métrica | Dos dispositivos vinculados presentan credenciales distintas entre sí y distintas de las del usuario; la revocación de la credencial de un dispositivo no afecta a ningún otro. |
| Origen | Atributo de calidad declarado en la Visión del producto. Fase de producción: Sprint 5. |
| Prioridad | Imprescindible (fase de producción) |
| Por qué importa | Una credencial compartida significa que comprometer un dispositivo compromete todos; y que retirar un dispositivo vendido exige cambiar la credencial de toda la flota. |
| Afecta a | RF-002, RNF-SEG-001 |

**Usabilidad**

**RNF-USA-001 · Efecto en máximo 3 toques**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Usabilidad |
| Descripción | Activar un efecto predefinido toma como máximo 3 toques desde la pantalla principal. |
| Métrica | Número de toques desde abrir la app hasta que el efecto se envía, contado en el flujo principal (seleccionar dispositivo → elegir efecto → aplicar); debe ser ≤ 3 sin contar ajustes opcionales. |
| Origen | Conflicto de usuarios: el flujo casual define el éxito del producto. Confirmado por el cliente. |
| Prioridad | Imprescindible |
| Por qué importa | El consumidor plug-and-play descarta la app si activar una luz exige más pasos que el interruptor de la pared. |
| Afecta a | RF-007 |

**RNF-USA-002 · Primer efecto en < 5 minutos**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Usabilidad |
| Descripción | Un usuario nuevo registra su primer dispositivo y activa su primer efecto en menos de 5 minutos, sin capacitación previa. |
| Métrica | Tiempo desde abrir la app por primera vez hasta ver el primer efecto en el dispositivo, medido con un usuario de prueba sin instrucciones más allá de la etiqueta del dispositivo (MAC). |
| Origen | Conflicto de usuarios: el consumidor plug-and-play no tolera fricción de onboarding. Confirmado por el cliente. |
| Prioridad | Importante |
| Por qué importa | El registro de dispositivos es el punto donde el usuario casual decide si el producto es para él o "es de makers". |
| Afecta a | RF-001, RF-002, RF-007 |

**Portabilidad e interoperabilidad**

**RNF-POR-001 · Navegadores modernos sin instalación**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Portabilidad |
| Descripción | El sistema funciona en las últimas dos versiones de Chrome, Firefox, Safari y Edge, en desktop y móvil, sin instalación. |
| Métrica | Los flujos principales (vincular dispositivo, activar efecto, streaming) se completan sin errores en cada navegador y plataforma listados; verificación por matriz de pruebas. |
| Origen | Tipo de sistema: progressive web app declarado en la Visión del producto. |
| Prioridad | Imprescindible |
| Por qué importa | Ser PWA es la alternativa al ecosistema cerrado de apps nativas; fallar en un navegador común contradice la razón de ser del sistema. |
| Afecta a | RF-007, RF-010 |

**RNF-INT-001 · Dispositivo nuevo sin modificar el sistema**

| Campo | Contenido |
|---|---|
| Atributo de calidad | Interoperabilidad |
| Descripción | Cualquier dispositivo que implemente el protocolo MQTT documentado puede vincularse y ser controlado sin modificar el código del sistema. |
| Métrica | Un dispositivo distinto al de desarrollo (distinto modelo o cantidad de LEDs) que implemente el protocolo documentado se vincula, reporta estado y recibe efectos y animaciones sin cambios en el código de la app. |
| Origen | Tipo de sistema: control genérico sobre un protocolo abierto; atributo declarado en la Visión del producto. |
| Prioridad | Imprescindible |
| Por qué importa | La propuesta de valor frente a las apps de fabricante es que el sistema sirve para cualquier dispositivo compatible; si cada dispositivo nuevo exige código nuevo, el sistema es otra app propietaria. |
| Afecta a | RF-002, RF-015 |



## 5. Casos de uso

Los casos de uso se trabajaron en la semana 7. El detalle de cada uno (actor, objetivo, precondiciones, escenario principal, flujos alternos y postcondición) está en `docs/casos de uso/cu-01.md` a `cu-16.md`. Cada caso de uso se relaciona con los requisitos funcionales que realiza:

| ID | Nombre | Requisitos que realiza |
|---|---|---|
| CU-01 | Registrar una cuenta | RF-001 |
| CU-02 | Iniciar sesión | RF-017 |
| CU-03 | Vincular un dispositivo | RF-002, RF-003, RF-005, RNF-USA-002 |
| CU-04 | Consultar el estado de un dispositivo | RF-004, RF-005, RF-006, RNF-REN-003 |
| CU-05 | Actualizar información del dispositivo | RF-018 |
| CU-06 | Activar un efecto predefinido | RF-007, RF-008, RF-011, RF-012, RNF-REN-002, RNF-USA-001 |
| CU-07 | Detener el efecto o animación en curso | RF-009, RF-012 |
| CU-08 | Transmitir una animación en vivo (streaming) | RF-010, RF-011, RNF-REN-001 |
| CU-09 | Crear una animación personalizada | RF-013, RF-014 |
| CU-10 | Enviar una animación guardada a un dispositivo | RF-015, RF-012 |
| CU-11 | Consultar escenas | RF-019, RF-021, RF-012 |
| CU-12 | Crear una escena | RF-020, RF-021 |
| CU-13 | Agregar colores favoritos | RF-022 |
| CU-14 | Actualizar el firmware de un dispositivo (OTA) | RF-016 |
| CU-15 | Agregar una habitación | RF-023 |
| CU-16 | Seleccionar la ubicación de un dispositivo | RF-024 |



## 6. Trazabilidad

| Requisito | Origen | Caso de uso | Elemento del prototipo |
|---|---|---|---|
| RF-001 | Visión del producto | CU-01 | Pantalla de registro e inicio de sesión (Sprint 3, pendiente) |
| RF-002 | Visión del producto | CU-02 | Modal "Agregar dispositivo" de la webapp |
| RF-003 | Visión del producto | CU-02 | Backend: validación de MAC única (Sprint 3, pendiente) |
| RF-004 | Visión del producto | CU-03 | Pestaña Dispositivos de la webapp |
| RF-005 | Visión del producto | CU-03 | Suscripción al estado del dispositivo + mensaje de última voluntad (webapp + firmware) |
| RF-006 | Visión del producto | CU-03 | Pantalla de estado detallado del dispositivo (webapp) |
| RF-007 | Conflicto de usuarios | CU-04 | Pestaña Efectos de la webapp |
| RF-008 | Visión del producto | CU-04 | Control de brillo de la webapp |
| RF-009 | Visión del producto | CU-05 | Botón "Detener" de la webapp |
| RF-010 | Visión del producto | CU-06 | Modo streaming de la webapp (frames RGBA) |
| RF-011 | Protocolo del dispositivo | CU-04, CU-06 | Comportamiento del firmware (verificado en hardware) |
| RF-012 | Caso de uso CU-04 | CU-04, CU-05, CU-08 | Validación de estado antes de enviar (pendiente) |
| RF-013 | Conflicto de usuarios | CU-07 | Editor de animaciones (Sprint 4, pendiente) |
| RF-014 | Visión del producto | CU-07 | Backend + DB: biblioteca de animaciones (Sprint 4, pendiente) |
| RF-015 | Visión del producto | CU-08 | Envío de animación guardada con adaptación de LEDs (Sprint 4, pendiente) |
| RF-016 | Visión del producto | CU-09 | Actualización OTA desde el estado del dispositivo (pendiente) |
| RF-017 | Caso de uso CU-02 | CU-02 | Pantalla de inicio de sesión (Sprint 3, pendiente) |
| RF-018 | Caso de uso CU-05 | CU-05 | Edición de nombre en detalles del dispositivo (pendiente) |
| RF-019 | Caso de uso CU-11 | CU-11 | Sección de escenas (pendiente) |
| RF-020 | Caso de uso CU-12 | CU-12 | Editor de escenas + persistencia en DB (pendiente) |
| RF-021 | Caso de uso CU-11 | CU-11, CU-12 | Aplicación de escena a dispositivos (pendiente) |
| RF-022 | Caso de uso CU-13 | CU-13 | Selector de color con favoritos (pendiente) |
| RF-023 | Caso de uso CU-15 | CU-15 | Gestión de habitaciones (pendiente) |
| RF-024 | Caso de uso CU-16 | CU-16 | Asignación de habitación en detalles del dispositivo (pendiente) |
| RF-025 | Decisión de diseño | CU-11 | Agrupación de escenas por habitación (pendiente) |
| RNF-REN-001 | Tipo de sistema | CU-06 | Streaming de frames (webapp + firmware) |
| RNF-REN-002 | Tipo de sistema | CU-04 | Envío de comandos (webapp) |
| RNF-REN-003 | Protocolo del dispositivo | CU-03 | Indicador de estado en la lista de dispositivos |
| RNF-SEG-001 | Atributo de calidad | CU-02 | Broker propio con ACL por topic (Sprint 5, pendiente) |
| RNF-SEG-002 | Atributo de calidad | CU-02 | Credenciales por dispositivo (Sprint 5, pendiente) |
| RNF-USA-001 | Conflicto de usuarios | CU-04 | Flujo principal de la pestaña Efectos |
| RNF-USA-002 | Conflicto de usuarios | CU-02 | Flujo completo de registro → vincular → efecto |
| RNF-POR-001 | Tipo de sistema | CU-04, CU-06 | PWA en navegadores (matriz de pruebas, Sprint 6) |
| RNF-INT-001 | Tipo de sistema | CU-02, CU-08 | Vinculación por protocolo documentado (docs/API.md) |


