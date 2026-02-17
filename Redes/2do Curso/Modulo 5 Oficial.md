# 1-Intro
El módulo se centra en cómo viaja el tráfico IP desde un dispositivo hasta otro, incluso cuando ese destino está en otra red o en Internet.

Aquí el foco ya no es solo enviar datos dentro de una red local, sino cómo se mueven los datos entre redes distintas, lo cual es la base del funcionamiento de Internet.

## Objetivos
Objetivos del Módulo

    - Revisión del Modelo OSI - Para identificar en qué capa operan diferentes protocolos y componentes
    - Comunicación de Capa de Red - Entender qué sucede en la capa 3 con IP
    - Protocolo ARP - Cómo funciona la resolución de direcciones
    - Puerta de enlace predeterminada - Su propósito para enrutar entre redes
    - Funcionamiento del enrutamiento IP - Creación de tablas de enrutamiento
    - Demostración de Traceroute - Visualizar enrutadores entre origen y destino

## Capas OSI Involucradas

El enrutamiento IP utiliza las 3 capas inferiores:

Capa 1 - Física: Medios de transmisión
Capa 2 - Enlace de Datos: Movimiento local (saltos pequeños)
Capa 3 - Red: Enrutamiento a través de Internet

    2. Capa de Enlace de Datos (Capa 2)
    Función: Mover tráfico en "pequeños incrementos" entre dispositivos
    Protocolo principal: Ethernet
    Dispositivo: Conmutador (Switch)
    Unidad de datos: Trama (Frame)
    Proceso: El switch crea conexiones entre dispositivos conectados a él

    3. Capa de Red (Capa 3)
    Función: Proporcionar el "mapa" completo para atravesar toda Internet
    Protocolo: IP (Protocolo de Internet)
    Dispositivo: Enrutador (Router)
    Propósito: Mover tráfico de un segmento de red a otro de manera eficiente

## EJEMPLO DETALLADO: Ruta de Estación de Trabajo a Servidor

1. Estación de Trabajo (Cliente)

Dispositivo de origen en la red doméstica

2. Enrutador Inalámbrico Doméstico

Primera parada del tráfico
Se representa con un círculo con flechas

3. Cable Módem (Puente de Capa 2)

Convierte tramas Ethernet → tramas DOCSIS
DOCSIS: Protocolo que usan los módems de cable para comunicarse con el ISP 
Proceso: Extrae el paquete IP de la trama Ethernet y lo coloca en una nueva trama DOCSIS (Internet Service Provider)

4. Internet (Múltiples Enrutadores)

Lleno de enrutadores que procesan el tráfico
Representación empresarial: círculo con flechas apuntando hacia adentro y afuera

5. Servidor (Destino)

Dispositivo final al que se quiere llegar

Flujo del Tráfico:
Estación de Trabajo → Router Doméstico → Cable Módem (conversión de tramas) 
→ Internet (múltiples routers) → Servidor


Conceptos Adicionales Importantes
Interacción Capa 2 y Capa 3:

Capa 2 maneja conexiones locales individuales
Capa 3 proporciona la visión completa del recorrido
Ambas trabajan juntas: cada "salto" usa Capa 2, pero la ruta completa requiere Capa 3

Diferencias de Representación:

Router doméstico: Dibujo realista del dispositivo
Router empresarial/Internet: Círculo con flechas (símbolo estándar en diagramas de red)


# ARP-Address Resolution Protocol

Desglose Detallado: Protocolo de Resolución de Direcciones (ARP)
Escenario de la Red
Red Simple:


Dispositivo A: 10.0.0.10
Dispositivo B: 10.0.0.20
Conectados a un enrutador
El enrutador conectado a Internet

Dos Modos de Operación:

Comunicación local: Entre 10.0.0.10 y 10.0.0.20 (mismo segmento)
Comunicación externa: A través del enrutador hacia Internet

Vamos a comenzar observando la comunicacion entre los 2 dispositivos internos

## Estructura del Paquete IP
Componentes del Paquete:
1. Datos ICMP (Protocolo de Mensajes de Control de Internet)

Usado por el comando ping
Envía mensaje y recibe respuesta

2. Paquete IP (contiene):

Dirección IP de origen
Dirección IP de destino
TTL (Time to Live / Tiempo de Vida): Valor = 128
Otra información adicional

3. El paquete anteriror se colocara dento de una Trama de Capa 2 (cambia frecuentemente en el recorrido):

Dirección MAC de destino
Dirección MAC de origen
Protocolo de Capa 3: IPv4


- ICMP - Protocolo de Mensajes de Control de Internet
    ¿Qué es?
    Es el protocolo que usa el comando ping. Vive dentro del paquete IP como los datos que se transportan.
    ¿Para qué sirve?
    
    Verificar si un dispositivo está vivo y respondiendo
    Diagnosticar problemas de red
    Reportar errores entre dispositivos
    
    ¿Cómo funciona el ping?
    PC A                          PC B
      |                             |
      | --- ICMP Echo Request  --→  |   "¿Estás ahí?"
      |                             |
      | ←-- ICMP Echo Reply    ---  |   "¡Sí, aquí estoy!"
    Tipos de mensajes ICMP comunes:
    MensajeSignificadoEcho RequestEl ping que envíasEcho ReplyLa respuesta al pingDestination UnreachableNo se pudo llegar al destinoTTL ExceededEl TTL llegó a 0, paquete descartadoTime ExceededLo usa Traceroute
    
## EJEMPLO COMPLETO: Proceso de Ping entre Dispositivos

- FASE 1: Creación del Paquete IP

- Comando ejecutado:

- ping 10.0.0.20


### FASE 1:

    IP Origen: 10.0.0.10
    IP Destino: 10.0.0.20
    TTL: 128 (establecido por el sistema operativo)

    ¿Qué hace el TTL?

    Es un contador que se reduce en 1 cada vez que pasa por un enrutador
    Si llega a 0, el paquete se descarta
    Propósito: Evitar que paquetes vivan infinitamente si hay bucles en la red
    Rango: 1 a 255
    Por defecto: 128 en la mayoría de sistemas operativos


### FASE 2: Creación de la Trama Ethernet

    Trama que necesitamos construir:
    [MAC Destino: ???] [MAC Origen: conocida] [Protocolo: IPv4] [Paquete IP]

Información que tenemos:

MAC Origen: Dirección MAC de 10.0.0.10 (nuestra estación)
Protocolo: IPv4
MAC Destino: ¡NO LA CONOCEMOS!

Problema: La estación de trabajo no sabe la dirección MAC de 10.0.0.20

Solución: Usar ARP (Protocolo de Resolución de Direcciones)

### FASE 3: Solicitud ARP (ARP Request)
    El mensaje se pone en espera mientras se resuelve la dirección MAC.
    Se crea una nueva trama ARP:
    Contenido de la solicitud:

    Pregunta: "¿Quién tiene 10.0.0.20?"
    Trama ARP Request:
    [MAC Destino: FF:FF:FF:FF:FF:FF] [MAC Origen: MAC de 10.0.0.10] [Protocolo: ARP] [¿Quién tiene 10.0.0.20?]

    Detalles importantes:

    MAC Destino = FF:FF:FF:FF:FF:FF: Dirección de broadcast (todas las F)

    Significa: "Todos los dispositivos deben recibir esto"


    Protocolo: ARP (es un protocolo de Capa 2, no Capa 3)
    Mensaje: Se envía a TODOS los dispositivos en el segmento de red

    ¿Qué pasa con los dispositivos que lo reciben?

    - Si NO tienen esa IP → Descartan el mensaje
    - Si SÍ tienen esa IP → Responden


### FASE 4: Respuesta ARP (ARP Reply)
    Dispositivo 10.0.0.20 responde:
    Trama ARP Reply:
    [MAC Destino: MAC de 10.0.0.10] [MAC Origen: MAC de 10.0.0.20] [Protocolo: ARP] [La MAC para 10.0.0.20 es XX:XX:XX:XX:XX:XX]
    Proceso:

    10.0.0.20 sabe quién le preguntó (porque la MAC origen venía en la solicitud)

    Crea una respuesta con su propia dirección MAC
    Envía la respuesta directamente a 10.0.0.10 (no broadcast)


### FASE 5: Envío del Ping Original

10.0.0.10 recibe la respuesta ARP:

    Extrae la dirección MAC de 10.0.0.20
    Completa la trama Ethernet del ping original:

    Trama final del Ping:
    [MAC Destino: MAC de 10.0.0.20] [MAC Origen: MAC de 10.0.0.10] [IPv4] [Paquete IP con ping]

    Envía el ping directamente a 10.0.0.20


    Concepto Clave: Caché ARP (Tabla ARP)
    ¿Qué es?

    Una tabla que mapea direcciones IP (Capa 3) a direcciones MAC (Capa 2)
    Se almacena en cada dispositivo con capacidades de Capa 3

    ¿Para qué sirve?

    Eficiencia: No tener que enviar solicitud ARP cada vez
    La próxima vez que 10.0.0.10 quiera comunicarse con 10.0.0.20, consulta la tabla directamente

Características:

Validez temporal: Solo dura minutos (90 segundos típicamente)
Después expira y se debe hacer nueva solicitud ARP
Razón: Permite que dispositivos cambien sus IPs sin problemas

Diferencias Importantes: Tabla ARP vs Tabla de Direcciones MAC
Tabla de Direcciones MAC (en Switches)

Ubicación: En switches (dispositivos Capa 2)
Mapeo: Puerto físico (Capa 1) → Dirección MAC (Capa 2)
Ejemplo: "Puerto 5 → MAC AA:BB:CC:DD:EE:FF"

Tabla ARP (en dispositivos con IP)

Ubicación: En computadoras, routers (dispositivos Capa 3)
Mapeo: Dirección IP (Capa 3) → Dirección MAC (Capa 2)
Ejemplo: "10.0.0.20 → MAC AA:BB:CC:DD:EE:FF"

NO son la misma tabla aunque ambas contengan direcciones MAC

¿Por Qué No Usar Broadcast para Todo?
Pregunta del ejemplo: "¿Por qué no enviar todo a broadcast?"
Respuestas:

Ineficiencia: Todos los dispositivos recibirían todo el tráfico
Sobrecarga del switch: Se saturaría fácilmente
Anula el propósito del switch: Los switches están diseñados para crear conexiones directas
Pérdida de rendimiento: Cada dispositivo tendría que procesar paquetes que no son para él

A   RP es la solución elegante:

    Solo se usa broadcast una vez para descubrir
    Después, toda comunicación es directa (unicast)



## Enrrutamiento IP
Internet funciona gracias a los enrutadores:

Internet está lleno de enrutadores interconectados
Cada enrutador tiene un "pequeño mapa" de cómo llegar a todas las redes
Mientras el mapa esté correcto y los enlaces activos, el tráfico fluye

Redes en el Ejemplo
    - 10.0.0.0/24 - Conectada al Router A
    - 172.16.0.0/30 - Entre Router A y Router B
    - 172.16.0.4/30 - Entre Router B y Router C
    - 192.168.10.0/24 - Conectada al Router C

## PROBLEMA: Intento de Ping SIN Tablas Completas
Escenario:

    Origen: 10.0.0.10
    Comando: ping 192.168.10.8
    Destino: 192.168.10.8

¿Qué pasa?
    En Router A:

    Recibe el paquete
    Busca en su tabla de enrutamiento
    Pregunta: "¿Sé cómo llegar a 192.168.10.0/24?"
    Respuesta: NO

Acción del Router A:

    Descarta el mensaje (lo tira)
    Opcionalmente, puede enviar un mensaje ICMP de regreso diciendo "No sé cómo llegar" (depende de la configuración)

Resultado: El ping FALLA

## Solucion Construir las tablas de enrrutamiento completas
SOLUCIÓN: Construir Tablas de Enrutamiento Completas

Concepto Clave:

Cada router necesita conocer:

    Todas las redes directamente conectadas (las tiene por defecto)
    Cómo llegar a las redes NO directamente conectadas


## PASO 1: Configurar Router A
Redes que Router A NO conoce:

172.16.0.4/30
192.168.10.0/24

Configuración manual:
    Ruta 1:
    Red destino: 172.16.0.4/30
    Siguiente salto: 172.16.0.2 (Router B, interfaz F0/0)

    Ruta 2:
    Red destino: 192.168.10.0/24
    Siguiente salto: 172.16.0.2 (Router B, interfaz F0/0)

Lógica:

- Router A NO está conectado directamente a Router C
- Pero SÍ está conectado a Router B
- Entonces envía todo al Router B y deja que Router B decida qué hacer después


## PASO 2: Configurar Router B
Redes que Router B NO conoce:
    10.0.0.0/24
    192.168.10.0/24

Configuración manual:

Ruta 1:
    - Red destino: 10.0.0.0/24
    - Siguiente salto: 172.16.0.1 (Router A, interfaz F0/0)

Ruta 2:
    Red destino: 192.168.10.0/24
    Siguiente salto: 172.16.0.5 (Router C, interfaz F0/0)
    Tabla de Enrutamiento COMPLETA de Router B:
Red                  Siguiente Salto / Interfaz
    - 10.0.0.0/24     →    172.16.0.1 (via Router A)
    - 172.16.0.0/30   →    F0/0 (directa)
    - 172.16.0.4/30   →    F0/1 (directa)
    - 192.168.10.0/24 →    172.16.0.5 (via Router C)



## PASO 3: Configurar Router C
Redes que Router C NO conoce:

10.0.0.0/24
172.16.0.0/30

Configuración manual:
Ruta 1:
    Red destino: 10.0.0.0/24
    Siguiente salto: 172.16.0.6 (Router B, interfaz F0/1)

Ruta 2:
    Red destino: 172.16.0.0/30
    Siguiente salto: 172.16.0.6 (Router B, interfaz F0/1)

Lógica:

- Router C envía ambas al Router B
- Router B decidirá si es para él o para pasarla a Router A

Tabla de Enrutamiento COMPLETA de Router C:
Red                  Siguiente Salto / Interfaz
10.0.0.0/24     →    172.16.0.6 (via Router B)
172.16.0.0/30   →    172.16.0.6 (via Router B)
172.16.0.4/30   →    F0/0 (directa)
192.168.10.0/24 →    F0/1 (directa)



# FLUJO EXITOSO: Ping con Tablas Completas
Comando: ping 192.168.10.8 desde 10.0.0.10

IDA (Request):
1. PC 10.0.0.10 → Router A:
    - PC consulta tabla de enrutamiento
    - 192.168.10.8 no está en mi red local
    - Usa default gateway: Router A
    - ARP para Router A
    - Envía trama con paquete IP

2. Router A:
    - Recibe trama
    - Extrae paquete IP
    - Consulta tabla: ¿Sé cómo llegar a 192.168.10.0/24?
    - SÍ → Siguiente salto: 172.16.0.2 (Router B)
    - TTL: 128 → 127
    - Crea nueva trama
    - Envía a Router B
3. Router B:
    - Recibe trama
    - Extrae paquete IP
    - Consulta tabla: ¿Sé cómo llegar a 192.168.10.0/24?
    - SÍ → Siguiente salto: 172.16.0.5 (Router C)
    - TTL: 127 → 126
    - Crea nueva trama
    - Envía a Router C
4. Router C:
    - Recibe trama
    - Extrae paquete IP
    - Consulta tabla: ¿Sé cómo llegar a 192.168.10.0/24?
    - SÍ → Directamente conectada a F0/1
    - TTL: 126 → 125
    - ARP para 192.168.10.8
    - Crea trama
- Envía a PC 192.168.10.8

5. PC 192.168.10.8:
    - Recibe el ping
    - Genera respuesta

VUELTA (Reply):
Ruta de regreso:

    192.168.10.8 → Router C → Router B → Router A → 10.0.0.10
    Router C conoce cómo llegar a 10.0.0.0/24 (vía Router B)
    Router B conoce cómo llegar a 10.0.0.0/24 (vía Router A)
    Router A tiene 10.0.0.0/24 directamente conectada



# Protocolos de Enrutamiento
1. RIP (Routing Information Protocol)
Tipo: Vector de Distancia
Características:

    - Muy antiguo (años 80)
    - Ya NO se usa
    - Muy lento
    - No muy bueno en su trabajo
    - Útil solo en redes antiguas poco exigentes


2. EIGRP (Enhanced Interior Gateway Routing Protocol)
Tipo: Vector de Distancia
Características:

    - Protocolo de Cisco
    - Disponible públicamente (cualquier empresa puede implementarlo)
    - En declive en algunos lugares, más usado en otros
    - Situación mixta en la industria

Significado: Protocolo de Enrutamiento de Puerta de Enlace Interior Mejorado

3. OSPF (Open Shortest Path First)
Tipo: Estado de Enlace (Link State)
Características:

    - Extremadamente popular
    - Estándar en redes empresariales
    - Muy usado en grandes empresas
    - Mantiene un mapa completo de todos los enlaces
    - Calcula la mejor ruta a través de la red

Significado: Primero la Ruta Abierta Más Corta

4. BGP (Border Gateway Protocol)
Tipo: Híbrido (Path Vector)
Características:

    - Usado en Internet pública
    - Mueve rutas entre empresas e ISPs
    - Como un "lenguaje de scripting" con muchos parámetros
    - Implementa contratos comerciales entre ISPs
    - Determina quién paga qué tráfico

Significado: Protocolo de Puerta de Enlace Fronteriza

# Categorías de Protocolos
Por Algoritmo:

## Vector de Distancia:

    RIP
    EIGRP
    Miden "distancia" a la red destino

    Vector de Distancia (Distance Vector)
    ¿Cómo funciona?
    Cada router solo sabe cuántos saltos hay hasta llegar a una red, sin importar el camino. Es como preguntarle a tu vecino cómo llegar a un lugar: él te dice la dirección pero no conoce el mapa completo.
    Analogía: Imagina que preguntas cómo llegar al aeropuerto y te dicen "son 3 calles a la derecha", sin saber si hay tráfico, semáforos o si es la ruta más rápida.

    RIP: Cuenta saltos (hops). Máximo 15 saltos. Si hay 16, considera que el destino es inalcanzable. Muy limitado y lento para actualizarse.
    EIGRP: Más avanzado, considera no solo saltos sino también ancho de banda y retraso de los enlaces para elegir la mejor ruta.

Desventaja clave: Solo conocen lo que sus vecinos les dicen, no tienen visión completa de la red.

## Estado de Enlace:
    OSPF
    Mantiene mapa completo de la red
    Calcula mejor ruta

    Estado de Enlace (Link State)
    ¿Cómo funciona?
    Cada router construye un mapa completo de toda la red. Conoce todos los routers, todos los enlaces y el estado de cada uno. Con ese mapa calcula por sí solo la mejor ruta.
    Analogía: Es como tener Google Maps. Ves toda la ciudad, sabes qué calles están congestionadas y calculas la ruta óptima tú mismo.

    OSPF: Cada router comparte información sobre sus propios enlaces con todos los demás routers de la red. Todos terminan teniendo el mismo mapa completo. Si un enlace falla, todos se enteran rápidamente y recalculan.

    Ventaja clave: Reacciona mucho más rápido a cambios en la red que los protocolos de vector de distancia.




## Híbrido:
    BGP
    Usa múltiples parámetros

    Híbrido (Path Vector)
    ¿Cómo funciona?
    BGP no encaja bien en las categorías anteriores. No solo mide distancia ni mantiene un mapa, sino que toma decisiones basadas en políticas y contratos comerciales entre organizaciones.
    Analogía: Es como un acuerdo entre países sobre por dónde puede pasar el tráfico aéreo. No siempre se elige la ruta más corta, sino la que cumple con los acuerdos establecidos.

    BGP: Usado en Internet entre ISPs y grandes empresas. Un ISP puede decir "el tráfico de esta empresa NO puede pasar por la red de tal país" o "prefiero este camino porque tenemos contrato con ese proveedor". Tiene decenas de parámetros configurables.


