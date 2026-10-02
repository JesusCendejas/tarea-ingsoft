# Guion de entrevista · MoonLightApp

**Sistema:** MoonLightApp — PWA de control de luces inteligentes (bocina Moon, lámparas y tiras LED compatibles con el protocolo MQTT)
**Autor:** Jesús Cendejas
**Técnica:** Entrevista

## Objetivo de la entrevista

El objetivo de esta entrevista es conocer cómo controlan actualmente las personas sus luces inteligentes y qué herramientas usan para hacerlo (apps nativas, servidores locales, editores, etc.).

También se busca conocer qué problemas se presentan al usar esas herramientas, qué reglas o costumbres tiene cada persona y qué cosas les gustaría mejorar o implementar.

Por otra parte, se quiere conocer cómo les gustaría llevar el control de sus dispositivos desde una página web, qué información les gustaría ver de cada aparato y qué necesitarían visualizar tanto los usuarios casuales como los makers que construyen o regalan sus dispositivos.

## 1. CONTEXTO

1. Cuéntame, ¿qué dispositivos de luces inteligentes tienes actualmente y cómo los controlas?
2. ¿Qué personas usan las luces en tu casa y cómo se organizan para controlarlas?
3. ¿Cómo accedes actualmente al control de tus luces cuando estás fuera de casa? ¿Y cuando estás dentro?
4. ¿Qué información necesitas tener disponible para saber que tus luces están funcionando bien?
5. ¿Qué tipos de dispositivos manejas? ¿Solo luces o también bocinas u otros aparatos?
6. ¿Cómo personalizas actualmente el color, el brillo o los efectos de tus luces?
7. ¿Qué reglas o costumbres tienes en casa para el uso de las luces (horarios, ambientes, quién puede cambiarlas)?
8. Cuando alguien nuevo llega a tu casa, ¿cómo le explicas cómo funcionan las luces y cómo se controlan?
9. *(Maker)* Cuéntame cómo construiste tu dispositivo. ¿Cómo lo configuraste la primera vez y qué fue lo más complicado?
10. *(Maker)* Cuando regalaste o quisiste compartir tu dispositivo, ¿cómo le explicaste a la otra persona cómo usarlo? ¿Qué problemas tuvo?

## 2. PROCESO ACTUAL

1. Cuéntame paso a paso qué sucede desde que quieres cambiar algo en tus luces hasta que lo ves funcionando.
2. ¿Cómo sabes si un dispositivo está encendido, conectado o funcionando correctamente?
3. ¿Cómo sabes en qué estado está cada uno de tus dispositivos (encendido, desconectado, mostrando algo)?
4. ¿Cómo creas o descubres nuevos efectos y animaciones para tus luces?
5. ¿Cómo guardas tus configuraciones favoritas para poder repetirlas después?
6. Después de configurar un efecto o color, ¿cómo verificas que el dispositivo lo recibió y lo está mostrando?
7. ¿En qué momento consideras que un cambio quedó aplicado y listo?
8. ¿Cómo compartes el control de las luces con otras personas de tu casa?
9. *(Maker)* ¿Cómo actualizas el firmware de tus dispositivos? ¿Qué tan seguido y qué tan complicado resulta?
10. ¿Cómo configuras el WiFi de un dispositivo nuevo o cuando cambias de red?

## 3. DOLORES

1. ¿Qué parte del control actual de tus luces te genera más trabajo o te resulta más complicada?
2. Cuéntame sobre algún problema que haya ocurrido al configurar o controlar tus luces.
3. ¿Qué tipo de errores o confusiones ocurren con mayor frecuencia?
4. ¿Qué información de tus dispositivos es la más difícil de consultar o mantener actualizada?
5. Cuando varias personas quieren controlar las luces al mismo tiempo, ¿cómo manejan la situación?
6. ¿Qué problemas llegan a tener con la conexión, los dispositivos que se desconectan o los cambios que no se aplican?
7. ¿Qué dificultades tienen al explicarle a alguien nuevo cómo usar las luces, los efectos o las animaciones?
8. Si pudieras mejorar algo de la forma en la que controlas tus luces actualmente, ¿qué sería y por qué?
9. *(Maker)* ¿Qué es lo que la gente a la que le regalaste un dispositivo no logra hacer sin tu ayuda?

## 4. EXCEPCIONES

1. ¿Qué haces cuando un dispositivo no responde o aparece como desconectado?
2. ¿Qué sucede cuando se cae el internet de tu casa? ¿Cómo se quedan las luces y cómo las recuperas?
3. ¿Qué haces cuando mandas un comando o un efecto y el dispositivo no lo muestra?
4. ¿Qué sucede si dos personas mandan comandos diferentes al mismo dispositivo al mismo tiempo?
5. ¿Qué haces cuando un dispositivo nuevo no se deja registrar o configurar?
6. ¿Qué sucede si actualizas el firmware de un dispositivo y algo sale mal?
7. Si cambias un dispositivo viejo por uno nuevo, ¿qué haces con tus animaciones y configuraciones guardadas?
8. ¿Hay alguna otra situación poco común que cambie la forma normal en la que controlas tus luces?

## 5. VERIFICACIÓN DE SUPUESTOS

En la primera versión de MoonLightApp se plantearon algunas ideas sobre cómo podría funcionar el sistema. Con estas preguntas se busca saber cuáles realmente serían útiles para las personas y cuáles tendrían que modificarse.

### Supuesto 1 · Registro de dispositivos

Pensando en una página web de control de luces, ¿cómo te gustaría registrar un dispositivo nuevo en tu cuenta? ¿Qué te parecería usar el código que viene en la etiqueta del aparato, y que solo se necesite una vez?

### Supuesto 2 · Estado de los dispositivos

¿Qué datos consideras necesarios para saber que un dispositivo está funcionando correctamente? ¿Qué te serviría ver de cada aparato: si está conectado, su IP, la calidad de su señal WiFi, la versión de su programa?

### Supuesto 3 · Efectos y brillo

¿Qué efectos predefinidos te gustaría tener disponibles y qué controles esperas encontrar (velocidad, intensidad, brillo, colores)?

### Supuesto 4 · Animaciones personalizadas

Durante el desarrollo de MoonLightApp se propuso un editor de animaciones frame a frame, donde tú creas la animación en la página y el dispositivo la reproduce en bucle.

- ¿Qué te parecería poder crear tus propias animaciones desde el navegador?
- ¿Qué tan importante es que las animaciones se guarden en el dispositivo y también en tu cuenta?
- Si un día cambias tu luna por otra, ¿te gustaría poder pasarle tus animaciones a la nueva?

### Supuesto 5 · Escenas y habitaciones

- ¿Qué te parecería poder guardar escenas que configuren varios dispositivos a la vez (efecto, color, brillo) y activarlas juntas?
- ¿Cómo te gustaría organizar tus dispositivos: por habitación, por tipo, libremente?

### Supuesto 6 · Concurrencia

Si dos personas abren la página al mismo tiempo y las dos tocan controles del mismo dispositivo, ¿qué crees que debería pasar? ¿Gana el último que tocó, o debería haber algún aviso o permiso?

### Supuesto 7 · Colores favoritos

¿Te parecería útil guardar tus colores favoritos para aplicarlos rápido? ¿Cuántos y cómo te gustaría organizarlos?

### Supuesto 8 · Actualizaciones (OTA)

*(Maker)* ¿Qué te parecería poder actualizar el firmware de tus dispositivos desde la propia página, sin cables ni programas extra? ¿Qué precauciones esperarías del sistema durante una actualización?

### Supuesto 9 · Configuración WiFi

¿Consideras correcto que el WiFi de los aparatos NO se configure desde MoonLight, sino que el aparato nuevo cree su propia red la primera vez y ahí se le meta la contraseña de tu casa? ¿Preferirías que la página también pudiera configurar el WiFi?

### Supuesto 10 · Editor para makers vs usuarios casuales

- Cuando quieres un efecto, ¿esperas encontrarlo listo en dos clics o prefieres un editor detallado?
- ¿Qué te parecería que el editor avanzado sea una capa aparte, para no complicar el uso diario?

## 6. CIERRE

1. De todo lo que hemos hablado, ¿hay algo que consideres que entendí mal o que debería aclarar mejor?
2. ¿Existe alguna costumbre o regla importante en tu casa sobre las luces que no te haya preguntado?
3. ¿Hay alguna situación que ocurra con tus dispositivos y que consideres importante tomar en cuenta para MoonLightApp?
4. ¿Hay alguna función que te gustaría encontrar en MoonLightApp y que no hayamos mencionado?


## BITÁCORA DE LA ENTREVISTA

**Fecha de aplicación:** lunes 21 de septiembre de 2026.
**Persona entrevistada:** Luz Yanelly Garduño / cliente (perfil usuario y maker)
**Duración:** 1 hora

### Supuestos confirmados

**Control sin instalar nada.** Se confirmó que el valor principal de MoonLight es abrir la página en el teléfono o la laptop y tener ahí todos los dispositivos, sin app nativa. El entrevistado lo contrasta de forma directa con la experiencia anterior — programa de escritorio y cable para la luna, app llena de anuncios y en inglés para la lámpara — y considera que el cambio a la página fue exactamente lo que quería.

**Registro de un dispositivo nuevo mediante el código de la etiqueta.** Se confirmó el flujo: el aparato trae un código impreso que se captura una sola vez, y después el dispositivo aparece siempre en la lista de la cuenta sin volver a registrarlo. El entrevistado lo vivió con la lámpara.

**Los efectos predefinidos bastan para el uso diario.** Se confirmó que la mayoría del uso se resuelve escogiendo un efecto existente (mencionó "luz de noche" como el de mayor uso, además de un efecto tipo vela y efectos de color). Los efectos se eligen en segundos y no requieren conocimiento técnico.

**Persistencia de las animaciones propias.** Se confirmó — y el entrevistado lo señaló como lo más valioso de todo — que las animaciones creadas quedan guardadas en el dispositivo y también en la cuenta, de modo que al cambiar un dispositivo viejo por uno nuevo se pueden pasar las animaciones sin rehacerlas.

**Concurrencia sin control: gana el último que toca.** Se confirmó el comportamiento actual. No hay aviso, ni permiso, ni bloqueo; cada usuario ve su propia pantalla como si estuviera solo y el dispositivo obedece el último comando recibido. El entrevistado describe que ocurre seguido porque comparte la cuenta con su hermano.

**La configuración de WiFi queda fuera de MoonLight.** Se confirmó como decisión correcta: el aparato crea su propia red la primera vez y ahí se captura la contraseña de la casa. El entrevistado lo describe como "un rollo aparte" que se hace una sola vez y que no quiere tener que explicar a terceros.

**Los efectos y las animaciones compiten y gana la animación.** Se confirmó: si está corriendo un efecto y se envía una animación, lo que se ve es la animación. El entrevistado lo aprendió por su cuenta al creer que un envío había fallado.

**La tensión entre usuario casual y maker.** Se confirmó con fuerza. El uso diario debe resolverse en dos clics con efectos listos; el editor detallado es una capacidad aparte, y hoy resulta hostil para quien no sabe de animación.

### Supuestos que resultaron falsos o que necesitan modificarse

**Se asumía que el estado del dispositivo ya estaba cubierto con conectado/desconectado.** Resultó falso. El dolor principal del entrevistado es que la página muestra los controles pero no el estado actual: no puede ver qué efecto, color o animación está corriendo en el aparato en ese momento. Esto lo obliga a deducir el estado tocando controles y observando qué pasa. Necesita modificarse: mostrar el estado real del dispositivo, no solo los controles.

**Se asumía que la página refleja el estado real del aparato.** Resultó falso. Cuando se cae el internet, la luna se queda encendida con lo último que tenía, pero la página la marca como desconectada; cuando el internet regresa, la página puede seguir diciendo "desconectada" hasta que el usuario recarga manualmente. Necesita modificarse: refresco o reconexión automática del estado.

**Se asumía que un dispositivo desconectado no recibe comandos.** Resultó parcialmente falso en la práctica: el dispositivo efectivamente no recibe nada, pero la página deja intentarlo sin impedirlo ni advertirlo con claridad. Necesita modificarse: bloquear o marcar de forma explícita los comandos cuando el dispositivo no está disponible.

**Se asumía que el editor de animaciones sirve para cualquier usuario.** Resultó falso. El entrevistado lo describe como "hecho para otra clase de persona": suelta todos los LEDs y todos los cuadros sin guía, y él tuvo que aprender a pura prueba y error. Necesita modificarse: plantillas o un modo guiado, dejando el editor detallado como capa separada.

**Se asumía que el alcance de la transferencia entre dispositivos eran las animaciones.** Queda por definir. El entrevistado no sabe si al cambiar de dispositivo también se transfieren el brillo, el color o el efecto actual, o únicamente las animaciones. Necesita precisarse antes de implementarlo.

**Se asumía que las escenas se explican solas.** Resultó falso. El entrevistado las menciona como una idea que suena bien pero que al tratar de explicarla en voz alta no le queda del todo clara, ni a él mismo. Necesita modificarse: definir y simplificar cómo se crean y se activan.

### Información inesperada

**La falta de confirmación de que un comando llegó.** Surgió de forma espontánea como una molestia recurrente: el entrevistado no tiene manera de saber si un cambio se aplicó o no, sobre todo cuando el dispositivo está inestable. La duda constante "¿llegó o no llegó?" lo lleva a reenviar comandos por si acaso.

**Una misma cuenta compartida por varias personas.** No existen cuentas por persona: el entrevistado y su hermano entran con la misma cuenta desde sus propios teléfonos, y también dio acceso a su prima. Esto cambia el modelo de acceso y explica por qué la concurrencia le importa más de lo previsto.

**No existe plan B si se pierde la etiqueta con el código de registro.** El entrevistado planteó la duda él mismo: si el código se pierde antes de registrar el dispositivo, no sabe qué pasaría ni qué alternativa habría.

**El valor percibido más alto no es el control en vivo, sino la conservación del trabajo propio.** Al preguntar por el cambio de dispositivo, lo que más le importó no fue la configuración ni los efectos, sino no perder las animaciones que creó, porque le costaron trabajo.

**La tolerancia a la concurrencia cambia al pensar en más usuarios.** En su casa, que gane el último no le molesta porque es su hermano y es una luz. Pero al imaginar regalar o vender el dispositivo, considera que el mismo comportamiento se vuelve un problema y pide al menos un aviso de que alguien más está controlando el dispositivo.

### Cambios que se realizarán en MoonLightApp

**Mostrar el estado actual del dispositivo.** Además de los controles, la interfaz debe indicar qué efecto, color o animación está corriendo en el aparato en ese momento. Es el cambio de mayor prioridad porque corresponde al dolor principal detectado.

**Actualización automática del estado.** La página debe reflejar por sí sola la desconexión y la reconexión del dispositivo, sin depender de que el usuario recargue manualmente.

**Comandos no enviables cuando el dispositivo está desconectado.** Cuando no haya conexión, la interfaz debe impedir el envío o marcarlo con claridad, en lugar de permitir que el usuario toque controles que no tendrán efecto.

**Confirmación de que un cambio se aplicó.** Se agregará una señal visible de que el comando llegó al dispositivo, para eliminar la incertidumbre de "¿llegó o no llegó?".

**Editor de animaciones accesible.** Se agregará un modo guiado o plantillas (por ejemplo girar, latir, parpadear) para usuarios sin conocimientos de animación, manteniendo el editor detallado como una capa aparte para quien sí lo quiera usar.

**Definir el alcance de la transferencia entre dispositivos.** Se precisará qué elementos se trasladan al cambiar de aparato — animaciones y también configuración de brillo, color o efecto — y se documentará en la interfaz.

**Aviso de uso concurrente.** Se evaluará notificar cuando otra persona esté controlando el mismo dispositivo, sin llegar a bloquear ni a pedir permiso para cada acción.

**Alternativa para el código de registro perdido.** Se definirá un procedimiento para registrar un dispositivo cuya etiqueta se perdió.

**Claridad en las escenas.** Se simplificará la creación y activación de escenas, y se revisará cómo se explican dentro de la propia interfaz.

### Conclusión de la entrevista

La entrevista confirmó que la decisión de fondo de MoonLight — una página web sin instalación, con los dispositivos de la persona siempre a la vista — es la correcta, y que los efectos predefinidos y la persistencia de las animaciones propias ya resuelven buena parte del uso diario. También confirmó el flujo de registro por código de etiqueta y la conveniencia de dejar la configuración de WiFi fuera del sistema.

Lo más valioso que salió de la entrevista fue una corrección de foco: el problema principal del usuario no es controlar las luces, sino saber qué están haciendo. La página muestra controles, no estado. De ahí se derivan los cambios prioritarios: mostrar qué está corriendo en el dispositivo, mantener ese estado actualizado sin recargar, avisar cuando el dispositivo no está disponible y confirmar que un comando se aplicó.

En segundo lugar quedó el editor de animaciones. La función existe y se usa, pero está construida para un perfil que no es el del usuario común; separar un modo guiado del editor detallado permite conservar la potencia sin que el uso diario se vuelva cuesta arriba.

También quedaron a la vista dos puntos que exigen definición antes de implementarse: qué se transfiere al cambiar de dispositivo y cómo se comporta el sistema cuando varias personas comparten una misma cuenta. Este último hoy es tolerable porque el usuario comparte la cuenta con su hermano, pero deja de serlo en el escenario de regalar o vender dispositivos, que es justamente uno de los objetivos de MoonLight.

Con esta información se pueden ajustar los requisitos de MoonLightApp y priorizar las funciones que realmente responden a lo que el usuario necesita, en lugar de las que solo amplían lo que el sistema ya hace.
