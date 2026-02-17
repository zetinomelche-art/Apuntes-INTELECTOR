# Dispositivos y Servicios de Capa 2

Se hablara hacerca de los modems y como estos comunican nuestra red local con el exterior

Tambien se habrara un poco hacerca de la configuracion de trafico en dispositivos de capa 2, como se le da prioridad a un servicio.

Protocolos de descubrimiento.

Solo trabajaremos con la capa 2 del modelo OSI,


# Modems

Su nombre proviene de MOdulador + DEModulador, podemos decir que su funciones es convertir seniales de un formato a otro para permitir la comunicacion entre 2 sistemas diferentes.


Modulador: dispositivo o circuito electrónico que superpone una señal de información (baja frecuencia/audio/video) sobre una señal portadora (alta frecuencia) para permitir su transmisión inalámbrica o por cable

Demodulador: circuito electrónico o dispositivo que extrae la información original (señal moduladora) de una onda portadora de alta frecuencia, realizando la operación inversa a la modulación


## MOdem original

El modem orignal, se conectaba a la linea telefonica de una casa, la cual a su vez se conectaba al computador.

Se usaba para conectaarse a BBS(Bulletin Board Service), lo que permitia enviar mensajes de texto, traferencia de archivos y chat basico, din embargo era muy lento y no podias llamar y hacer otras cosas al mismo tiempo.


## Modem actual

## Cable modem

- Protocolo que usa: DOCSIS (Data Over Cable Service Interface Specification)
- Protocolo de Capa 2 diseñado para transmitir datos por cable coaxial (el mismo cable de TV)

Que hace?
Pasar del protocolo DOCSIS que usa el ISP a  Ethernet Para nuestros disposivos.

Conversión:
Entrada: Señal DOCSIS (del proveedor de internet)
Salida: Ethernet (para nuestros dispositivos)

## Módem de Fibra Óptica

Tiene un nombre mas preciso que es: Convertidor de Medios (Media Converter)

Que hace?

Red del ISP(Fibra Optica) Ethernet Fibra -> [Modem] -> Ethernet

Convierte:

Entrada: Ethernet sobre fibra óptica (del ISP)
Salida: Ethernet sobre cable de cobre (para nuestros dispositivos)

- CAracteristicas:

Características:

    - Puerto de fibra óptica que conecta al ISP
    - Puerto de cobre Ethernet para conectar dispositivos internos
    - Se puede conectar a un access point inalámbrico
    - Suele incluir funciones extra como firewall para protección

## Modem DSL (Digital Subscriber Line)
Línea de Suscriptor Digital

que hace >
Conversión:

Entrada: Señal DSL (por el cable telefónico)
Salida: Ethernet (para nuestros dispositivos)

Popular a finales de los 90s y principios de los 2000s
Antes de que existiera la infraestructura de cable y fibra
Velocidades: ~1 a 2 Mbps (muy lento para estándares actuales)

POr que se ustiliza docsis?
Respuesta Simple
Porque el ISP necesita enviar datos por cable coaxial, que es la misma infraestructura física que ya existía para la televisión por cable. DOCSIS es el protocolo diseñado específicamente para ese tipo de cable.

La Razón Real: Reutilización de Infraestructura
El problema que resolvió DOCSIS:
Las empresas de cable ya tenían millones de kilómetros de cable coaxial instalado en hogares y negocios para dar servicio de TV por cable.


# Traffic Shaping (Configuracion de trafico)
Se refiere a una tacnico que permite dar prioridad a cierto tipo de trafico sobre otro en la red.

- El problema que resuelve:

Tipo de Tráfico         |Tolerancia a Retrasos               |Por que?
VoIP (llamada de voz)   |Ninguna                             |Es en tiempo real, los paquetes perdidos no se recuperan
Videollamada            |Muy poca                            |También es en tiempo real
YouTube / Streaming     |Alta                                |Puede almacenarse en caché antes de reproducirse
Descarga de archivos    |Alta                                |No importa si tarda un poco más

Como se usa:

Método 1: Código Especial en el Encabezado

    Se agrega una marca de prioridad en la información del encabezado del paquete IP
    Los switches y routers leen esa marca
    Procesan primero los paquetes marcados como alta prioridad
    Ejemplo: Campo DSCP/ToS en el paquete IP (lo vimos en el "Other" del paquete IP)

Método 2: Prioridad por VLAN
    Se configura el switch para dar prioridad a ciertas VLANs sobre otras
    Ejemplo: La VLAN de teléfonos tiene prioridad sobre la VLAN de computadoras
    Se hace directamente en la configuración del switch

- Otros Usos del Traffic Shaping

1. Limitación de Ancho de Banda
Ejemplo del instructor:

Contratas internet de 50 Mbps con tu ISP (Internet Service Provider)
Pero los cables Ethernet son de 100 Mbps o 1 Gbps (no hay de 50 exactos)

Solucin:

Traffic Shaping limita artificialmente el enlace a 50 Mbps
Así el ISP puede cobrar por el ancho de banda exacto contratado

# Protocolos de Descubrimiento de Vecinos

Es una funcion de la capa 2 que permite a los dispositivos anunciarse con sus dispositivos adyacentes directamente conectados, compartiendo informacion sobre si mismos

Que problema resuelve:
En una red con muchos dispositivos (routers, switches, firewalls), es muy fácil perderse en el caos de cables y conexiones, especialmente cuando:

    - No hay documentación actualizada
    - Un cable se desconectó y reconectó mal
    - Hay comportamiento inusual en la red
    - Se hereda una red sin documentar

Pregunta común del administrador:

    Qué dispositivo está conectado a este puerto?

        - Sin descubrimiento de vecinos: Hay que rastrear físicamente cada cable
        - Con descubrimiento de vecinos: El dispositivo te lo dice automáticamente 

¿Cómo Funciona?

Proceso básico:
    Paso 1: El dispositivo A envía un mensaje de Capa 2 a sus vecinos diciendo:
        "Hola, soy un Router
        Tengo estas capacidades: [lista]
        Te estoy enviando esto por el puerto X"
    Paso 2: El dispositivo B que recibe el mensaje responde:
        "Gracias, te agrego a mi tabla.
        Por cierto, yo soy un Switch
        Tengo estas capacidades: [lista]"
    Paso 3: Ambos dispositivos guardan la información en su tabla de vecinos



Protocolos de Descubrimiento de Vecinos
1. LLDP - Link Layer Discovery Protocol
Nombre completo: Protocolo de Descubrimiento de Capa de Enlace
Características:

    Estándar abierto (no pertenece a ninguna empresa)
    Compatible con cualquier fabricante
    Funciona en dispositivos no Cisco
    Diseñado para redes multivendor

Cuándo usarlo:

    Redes con equipos de diferentes marcas
    Ambientes donde se evitan protocolos propietarios


2. CDP - Cisco Discovery Protocol
Nombre completo: Protocolo de Descubrimiento de Cisco
Características:

    Habilitado por defecto en todos los dispositivos Cisco
    Protocolo muy simple y ligero
    Tan popular que algunos dispositivos no Cisco también lo usan
    Ampliamente implementado en la industria

Cuándo usarlo:

    Redes con equipos principalmente Cisco
    Cuando ya está habilitado por defecto (no requiere configuración)