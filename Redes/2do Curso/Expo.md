# CASMA/CD

Es un protocolo de red utilizado principalmente en Ethernet para gestionar la transmisión de datos en un medio compartido.

Muchos dispositivos comparten el mismo medio, escuchan antes de hablar y detectan si ocurre una colisión.

### ¿Se usa CSMA/CD hoy en día?
- Hoy no hablamos ni usamos CSMA/CD en redes Ethernet modernas
- Es una tecnología arcaica

### Cómo funcionaba el Ethernet original
    - El medio físico
    - Se usaba un cable coaxial grueso
    - Un solo cable
    - Todos los dispositivos conectados al mismo cable
    - No había switches, ni enlaces dedicados.

### Acceso múltiple (Multiple Access)

Muchos dispositivos compartían el mismo cable
Todos podían enviar y recibir datos por ese cable

Detección de portadora (Carrier Sense)


### Antes de enviar datos:
    - El dispositivo escucha el cable
    - Verifica si alguien más está transmitiendo
    - Si nadie habla → envía datos
    - Esto evita hablar encima de otro… en teoría.

### Cómo se transmitían los datos
    Los datos eran señales eléctricas

    Específicamente:
    +5 voltios = un dispositivo transmitiendo


### Colisiones
Ejemplo:
Si:

Dos dispositivos escuchan
Ambos creen que el cable está libre
Ambos transmiten al mismo tiempo

Entonces:
+5V + +5V = +10 voltios
Ese pico de 10 voltios es una colisión.

Cada dispositivo:
Detecta el pico de voltaje
Sabe que ocurrió una colisión
Detiene la transmisión

Los dispositivos esperan un tiempo aleatorio:

Vuelven a escuchar el cable
Si está libre → retransmiten los datos
El tiempo aleatorio evita que choquen otra vez inmediatamente.


“CSMA/CD fue fundamental en el diseño original de Ethernet, permitiendo que múltiples dispositivos compartieran un mismo medio físico. Sin embargo, con la llegada de los switches y enlaces dedicados, las colisiones prácticamente desaparecieron, haciendo que CSMA/CD hoy sea más un concepto histórico que una tecnología activa.”

## Duplex and Speed

Duplex:
Capacidad de un dispositivo para enviar y recibir datos, ya sea de forma simultánea (full-duplex) o alterna (half-duplex)

### Tipos de comunicación dúplex en Ethernet


En Ethernet existen dos modos de comunicación:

- Half-Duplex (Semidúplex)

- Full-Duplex (Dúplex completo)

### Half-Duplex (Semidúplex)

¿Cómo funciona?

- Solo un dispositivo puede transmitir a la vez
- El otro debe esperar
- No se puede enviar y recibir datos simultáneamente.

#### Ejemplo del video, Walkie-talkie

Este ejemplo es perfecto para la exposición:

- Presionas el botón → hablas

- Mientras hablas → no puedes escuchar

- La otra persona debe esperar

- Exactamente así funcionaba el Ethernet original.


#### Colisiones en semidúplex moderno (caso raro)

El video menciona algo importante:

Si:
- La comunicación es semidúplex
- El cable es demasiado largo
- PC y switch transmiten al mismo tiempo

Entonces:
- Puede ocurrir una colisión
- Se produce un pico de voltaje
- Esto hoy es muy poco común.




### Full-Duplex (Dúplex completo)
¿Cómo funciona?
Ambos dispositivos pueden:

- Enviar

- Recibir

- Al mismo tiempo

- No hay que turnarse.


#### Ejemplo del video: Teléfono

Muy buen ejemplo:

Puedes hablar mientras la otra persona habla

Puedes decir:

“ajá”

“sí”

“te escucho”

Sin interrumpir la comunicación

Eso es full-duplex.


### Full-Duplex en Ethernet moderno

Cuando conectamos una PC a un switch:
Hay dos canales de comunicación:
PC → Switch
Switch → PC

Cada dirección tiene su propio canal.

¿Puede haber colisión aquí?

No, porque:

- No comparten el mismo canal
- No hay competencia por el medio
- No existe el escenario de colisión clásica.



### Full-Duplex en Ethernet moderno

Cuando conectamos una PC a un switch:
Hay dos canales de comunicación:
PC → Switch
Switch → PC

Cada dirección tiene su propio canal.

¿Puede haber colisión aquí?

No, porque:

- No comparten el mismo canal
- No hay competencia por el medio
- No existe el escenario de colisión clásica.




### Velocidades Ethernet y sus nombres

Aquí entramos a algo clave para exámenes y exposiciones

Nombre	            | Velocidad
Ethernet	        | 10 Mbps
Fast Ethernet	    | 100 Mbps
Gigabit Ethernet	| 1 Gbps
10 Gigabit Ethernet	| 10 Gbps
40 Gigabit Ethernet	| 40 Gbps


Relación velocidad ↔ dúplex

- Este punto es clave :

Para:

- 1 Gbps
- 10 Gbps
- 40 Gbps

Es obligatorio usar full-duplex

Entonces… ¿CSMA/CD sigue existiendo?

- Sí, técnicamente sigue ahí:



“Ethernet originalmente funcionaba en modo semidúplex, lo que hacía necesarias las colisiones y el uso de CSMA/CD. Sin embargo, las redes modernas operan en full-duplex con enlaces dedicados y altas velocidades, eliminando prácticamente las colisiones y haciendo que CSMA/CD sea hoy más un concepto histórico que una preocupación real.”


## Ethernet II FRAME

Una trama ethernet es el conedor que usamos para enviar informacion a traves de una red ethernet. No se envian los datos sueltos, se "empaquetan" en una trama para que los dispositivos puedan: leeros, interpretarlos y decirdir que hacer con ellos.

## Ethernet II FRAME

¿Qué es una trama Ethernet?

Una trama Ethernet es el contenedor que usamos para enviar información a través de una red Ethernet.

- No enviamos datos “sueltos”.
- Los empaquetamos en una trama para que los dispositivos Ethernet puedan:

    - Leerlos
    - Interpretarlos
    - Decidir qué hacer con ellos

Si un dispositivo no entiende el formato Ethernet, no puede procesar la trama.



