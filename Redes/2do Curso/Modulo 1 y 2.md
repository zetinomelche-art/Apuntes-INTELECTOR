# Modulo 1-Phisical Layer Technologies


En la capa fisica hay 3 formas de mover los datos
    - Cableado de cobre
    - Fibra Optica
    - Wireles

# Modulo 2-xCableado de cobre

Este a su ves se subdivide en 2 categorias

## De par trenzado (Twisted Pair)
Se usa por que podemos tranportar gran cantidad de datos.

La razon de por que son trenzado es para evitar interferencias de campos magneticos, conocido como diafonia.

- Se hay cables con blindaje para evitar interferencias externas

### Categorias

Cat 1       -> Dorbell
Cat 3       -> Telefono /10Mbps
Cat 5       -> 100Mb
Cat 6       -> Gb Ethernet, se aumentarion las specs y se le agrego al una cruz de plastico al centro.
Cat 6a/7    -> 10Gb
Cat 8       -> 10 Gb

### RJ-11
Conector utilizado para telfono, cat-3. Un conector de solo 4 hilos, pa

### RJ-45
Tiene 8 pines

Orientacion ->

1   -> Transmit +
2   -> Transmit -
3   ->  Recieve +
4   ->
5   ->
6   ->  Recieve -
7   ->
8   -> 

- Cable cruzado
    Conectar router con ruoutwr
    Conectar Switchs con switch
    Conectar pc con pc

- Auto-MFI-X (Auto mediun dependent interface crossover)
Casi todos los disposivios usan esta tecnologia, significa que si el dispositivo tiene esta tecnologia no tienes que precuparte por el cable 

## Coaxial
- El cable fisico se llama RG-6
- El conectar el F-Type Connector

Twinaxial Cable
En centros de datos, para tranmitir datos 10Gb o hasta 40 Gb


## Fibra Optica

### Fibra Mono-modo
Se utlizan materiales muy estrictos encuanto a calidad, para que el pulso de luz recorra el tubo lo mas recto posibles, haciendo que la atenuacion sea menor, perfecto para grandes distancias.

### Fibra Multimodo
Tiene una un poco menos de calidad que la anterior, el tubo es mas grueso, pero es mas economica y perfecta para distancias no tan prolongadas. La luz tiende a rebotar mas en el tubo.

### Comprativa

Laser Type  | Wavelength    | Fiber         | Dsitance
LX          | 1270 - 1610nm | Single Mode   | 70 k 
SX          | 770 - 860 nm  | Multi mode    | 1/2 - 1 km

### OPtical Netwotk Interface Card

- GBIC
- SFT
- SFP+
- QSFP
- QSFP+

### Tipos de conectores

- ST Connector
- SC Connector
- LC Connector
Comun en redes modernas, se conecta a SFT

- MTRJ Connector
- FC Connector

### Angled Physical Contact (APC)
Es el angulo en que tiene que estar cortada la fibra para poder hacer un buen contacto y permitir el paso de la luz de manera correcta

### Ultra Phisical Contact (UPC)


### Simplex Pair
Es una de las maneras en que se conectan 2 dispositivos, ejemplo un switc, se usan una fbra para ir de A -> B y otra para ir de A -> A

### Bidireccional

Funciona con un solo cable, por lo que para lograr la comunicaion usa 2 hondas de luz diferentes. Para eso se usa algo llamado:

- Wave Division Multiplexing (WDM) - Multiplexación por división de ondas


# Capitulo 3-Ethernet Therms and Concepts

Este capitulo se centra mas que todo en enteer como funciona la capa 2 del modelo OSI, Data Link Layer.

La capa 2, es la emacrgada de mover los datos de un dispositivo a otro con exito.

La mayoria de redes comerciales y domesticas hacen uso de algun tipo de ethernet


Se enfoca mas en la parte conceptual y bases del funcionamiento.


## Ethernet está en todas partes:
- Redes empresariales
- Redes domésticas

- Ethernet en el hogar

    En casa solemos tener un dispositivo como:
    Un módem-router
    Con:
    Punto de acceso Wi-Fi
    Switch Ethernet integrado


- Ethernet en entornos empresariales

Ejemplos:

    Switches Cisco Catalyst de 48 puertos
    Puertos SFP para fibra óptica
    Conexiones de alta velocidad

Los SFP permiten:

    Conectar fibra óptica
    Usar distintos tipos de láser
    Ampliar distancia y velocidad
    
Define cómo se envían los datos, cómo se identifican los dispositivos mediante direcciones MAC y cómo se asegura que la información llegue correctamente de un punto a otro.


Ethernet es la tecnología de red más utilizada en el mundo para la comunicación de datos. Está presente en casi todos los entornos: hogares, empresas, universidades y centros de datos. Desde conectar una computadora a un router en casa hasta interconectar cientos de servidores en una empresa, Ethernet es la base sobre la que funcionan la mayoría de las redes modernas.



## CSMA/CD (Carrier Sense Multiple Acces with Collision Detection)

NO se habla ni se usan mucho a dia de hoy.

Muchos dispositivos comparten el mismo medio, escuchan antes de hablar y detectan si ocurre una colisión.



    


### ¿Se usa CSMA/CD hoy en día?
- Hoy no hablamos ni usamos CSMA/CD en redes Ethernet modernas
- Es una tecnología arcaica

### Cómo funcionaba el Ethernet original
El medio físico

Se usaba un cable coaxial grueso

Un solo cable

Todos los dispositivos conectados al mismo cable

No había switches, ni enlaces dedicados.


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

¿Por qué hablar de dúplex y velocidad?

Este tema responde la gran pregunta:
¿Por qué CSMA/CD ya no describe Ethernet como antes?

La respuesta corta (para la expo):

Porque ya no trabajamos en medio dúplex ni en medios compartidos.

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

Los dispositivos aún “escuchan” el medio

Pero:

- El canal casi siempre está libre

- No hay colisiones reales

CSMA/CD existe más como herencia histórica.

“Ethernet originalmente funcionaba en modo semidúplex, lo que hacía necesarias las colisiones y el uso de CSMA/CD. Sin embargo, las redes modernas operan en full-duplex con enlaces dedicados y altas velocidades, eliminando prácticamente las colisiones y haciendo que CSMA/CD sea hoy más un concepto histórico que una preocupación real.”

## Ethernet II FRAME

¿Qué es una trama Ethernet?

Una trama Ethernet es el contenedor que usamos para enviar información a través de una red Ethernet.

- No enviamos datos “sueltos”.
- Los empaquetamos en una trama para que los dispositivos Ethernet puedan:

    - Leerlos
    - Interpretarlos
    - Decidir qué hacer con ellos

Si un dispositivo no entiende el formato Ethernet, no puede procesar la trama.

### Estructura general del marco Ethernet

Una trama Ethernet está compuesta por tres grandes partes:

- Encabezado (Header – Capa 2)
- Datos (Payload / Carga útil)
- Pie de trama (Trailer)


### Encabezado Ethernet (Data Link Header)

El encabezado Ethernet contiene tres campos fundamentales:

1. Dirección MAC de destino

    Indica a qué dispositivo va dirigida la trama
    Es una dirección de Capa 2

2. Dirección MAC de origen

    Indica quién envió la trama
    También es una dirección de Capa 2

3. Campo Tipo (Type)

    Indica qué tipo de datos viajan dentro de la trama
    Sirve para saber a qué protocolo entregar la información

Este encabezado es lo que permite que Ethernet funcione correctamente.

# Campo Tipo (EtherType)

El campo de tipo indicará qué tipo de datos se están moviendo aquí o al menos qué protocolo se está utilizando para transportar los datos que están en el mensaje. Entonces, si es un paquete IP, tendrá un cierto
tipo de código; si es un paquete IP versión 6, tendrá un código de tipo
determinado; si es un mensaje ARP, tendrá un tipo de código determinado

“Oye, lo que viene dentro es…”


Este tipo de codigo le indica a nuestro SO qqué tipo de mensaje
está a punto de llegar y a qué sistema de software pasarlo.

Ejemplos:

IPv4
IPv6
ARP

racias a este campo:
La NIC
El sistema operativo

saben a qué parte del software enviar los datos.

Ejemplo práctico

Si el campo Tipo dice:

IPv4 → va al stack IP
ARP → va al proceso ARP

Sin este campo, el sistema no sabría cómo interpretar los datos.

### Carga útil (Payload)

La carga útil es:

La información que realmente queremos enviar

Normalmente contiene:

Un paquete de Capa 3 (IP)

Importante:

Capa 2 = Trama

Capa 3 = Paquete

No siempre hay un paquete IP:

Algunos mensajes son solo de Capa 2 (como ARP)


### FCS – Frame Check Sequence

Este es el pie de la trama.

Contiene:

CRC (Cyclic Redundancy Check)

¿Qué es el CRC?

Es un algoritmo matemático que:

Toma toda la trama:

    - MAC destino
    - MAC origen
    - Tipo
    - Datos
    - Genera un valor de 32 bits

Ese valor se coloca en el campo FCS

- Verificación en el receptor

Cuando el receptor recibe la trama:

    Calcula su propio CRC
    Lo compara con el FCS recibido
    Si coinciden → trama válida
    Si no coinciden → se descarta la trama

Ethernet:

    - NO retransmite tramas
    - NO avisa si algo falló

La recuperación depende de protocolos superiores, como:
TCP (Capa 4)


### MTU – Maximum Transmission Unit
¿Qué es la MTU?

Es el tamaño máximo de datos que puede transportar una trama

En Ethernet:

MTU = 1500 bytes

#### Jumbo Frames (Tramas gigantes)

MTU mayor a 1500 bytes

Usadas principalmente en:

- Centros de datos

- Redes de almacenamiento (SAN)

Ventajas:

- Menos tramas

Mayor eficiencia

- Requisito:

Todos los dispositivos deben soportarlas

Si no:

Se descartan

O causan errores

### PDU – Protocol Data Unit

El marco Ethernet completo se llama:

Unidad de Datos de Protocolo (PDU)

En la práctica diaria:
    Los ingenieros dicen “trama”

En documentación técnica:
    Verás PDU