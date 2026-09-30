## Requerimientos funcionales

****Cuentas y dispositivos****

-   ****RF-01**** · El sistema registra una cuenta de usuario nueva con correo y contraseña.
-   ****RF-02**** · El sistema vincula un dispositivo a la cuenta del usuario usando la dirección MAC como identificador único.
-   ****RF-03**** · El sistema impide vincular una misma MAC a dos cuentas distintas.
-   ****RF-04**** · El sistema muestra la lista de dispositivos vinculados al usuario con su estado (conectado / desconectado).
-   ****RF-05**** · El sistema marca como desconectado cualquier dispositivo que deje de reportar su estado.
-   ****RF-06**** · El sistema muestra el estado detallado del dispositivo seleccionado: IP, MAC, RSSI, memoria libre y versión de firmware.

****Control de iluminación****

-   ****RF-07**** · El sistema envía al dispositivo seleccionado un efecto predefinido con sus parámetros: velocidad, intensidad, brillo y paleta de colores.
-   ****RF-08**** · El sistema ajusta el brillo del dispositivo en un rango de 0 a 255.
-   ****RF-09**** · El sistema detiene el efecto o animación en curso cuando el usuario lo indica.
-   ****RF-10**** · El sistema envía frames de animación RGBA en modo streaming al dispositivo seleccionado.
-   ****RF-11**** · Cuando un efecto y un streaming se envían sobre el mismo dispositivo, el sistema ejecuta el último comando recibido.
-   ****RF-12**** · El sistema impide enviar comandos a un dispositivo marcado como desconectado.

****Editor y animaciones****

-   ****RF-13**** · El sistema permite diseñar una animación personalizada como secuencia de frames, definiendo color por LED y duración por frame.
-   ****RF-14**** · El sistema guarda las animaciones personalizadas en la cuenta del usuario.
-   ****RF-15**** · El sistema permite enviar una animación guardada a cualquier dispositivo vinculado a la cuenta, aunque no sea el dispositivo donde se creó.

****Actualizaciones****

-   ****RF-16**** · El sistema ofrece actualización de firmware OTA únicamente para dispositivos propietarios.


****Cuentas y sesión****

-   ****RF-17**** · El sistema autentica al usuario con su correo y contraseña y abre su sesión.
-   ****RF-18**** · El sistema permite editar el nombre de un dispositivo vinculado.

****Escenas****

-   ****RF-19**** · El sistema muestra las escenas guardadas en la cuenta del usuario.
-   ****RF-20**** · El sistema guarda una escena con la configuración de varios dispositivos (efecto, animación, color, brillo) para activarla en conjunto.
-   ****RF-21**** · El sistema aplica una escena enviando a cada dispositivo incluido su configuración guardada.

****Personalización****

-   ****RF-22**** · El sistema guarda colores favoritos en la cuenta del usuario, disponibles en el selector de color de todos sus dispositivos.

****Habitaciones****

-   ****RF-23**** · El sistema registra habitaciones en la cuenta del usuario para organizar sus dispositivos y escenas por ubicación.
-   ****RF-24**** · El sistema asigna un dispositivo a una habitación y lo muestra agrupado por ubicación en la lista de dispositivos.
-   ****RF-25**** · El sistema agrupa las escenas de la cuenta por habitación.
## Requerimientos no funcionales

****Rendimiento****

-   ****RNF-01**** · El streaming de animación sostiene 30 frames por segundo sin saltos visibles con el dispositivo en la misma red que el broker.
-   ****RNF-02**** · El tiempo entre que el usuario toca un control y el dispositivo reacciona es menor a 500 ms con conexión a internet normal.
-   ****RNF-03**** · Un cambio de estado del dispositivo (conectado ↔ desconectado) se refleja en la interfaz en menos de 30 segundos.

****Seguridad****

-   ****RNF-04**** · Un usuario solo puede publicar y suscribirse a los topics MQTT de sus propios dispositivos; cualquier intento sobre un topic ajeno es rechazado por el broker. __(Fase de producción — Sprint 5.)__
-   ****RNF-05**** · Cada dispositivo usa credenciales MQTT únicas, distintas de las de cualquier otro dispositivo. __(Fase de producción — Sprint 5.)__

****Usabilidad****

-   ****RNF-06**** · Activar un efecto predefinido toma como máximo 3 toques desde la pantalla principal.
-   ****RNF-07**** · Un usuario nuevo registra su primer dispositivo y activa su primer efecto en menos de 5 minutos, sin capacitación previa.

****Portabilidad e interoperabilidad****

-   ****RNF-08**** · El sistema funciona en las últimas dos versiones de Chrome, Firefox, Safari y Edge, en desktop y móvil, sin instalación.
-   ****RNF-09**** · Cualquier dispositivo que implemente el protocolo MQTT documentado puede vincularse y ser controlado sin modificar el código del sistema.