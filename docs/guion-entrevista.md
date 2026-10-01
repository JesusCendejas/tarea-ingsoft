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
**Persona entrevistada:** Luz Yaneli / Cliente
**Duración:** 1 hora

### Supuestos confirmados



### Supuestos que resultaron falsos o que necesitan modificarse



### Información inesperada



### Cambios que se realizarán en MoonLightApp



### Conclusión de la entrevista

