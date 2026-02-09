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
Proceso: Extrae el paquete IP de la trama Ethernet y lo coloca en una nueva trama DOCSIS

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


## EJEMPLO COMPLETO: Proceso de Ping entre Dispositivos
FASE 1: Creación del Paquete IP

Comando ejecutado:

ping 10.0.0.20


Paquete IP generado:

IP Origen: 10.0.0.10
IP Destino: 10.0.0.20
TTL: 128 (establecido por el sistema operativo)

¿Qué hace el TTL?

Es un contador que se reduce en 1 cada vez que pasa por un enrutador
Si llega a 0, el paquete se descarta
Propósito: Evitar que paquetes vivan infinitamente si hay bucles en la red
Rango: 1 a 255
Por defecto: 128 en la mayoría de sistemas operativos


FASE 2: Creación de la Trama Ethernet
Trama que necesitamos construir:
[MAC Destino: ???] [MAC Origen: conocida] [Protocolo: IPv4] [Paquete IP]
Información que tenemos:

✅ MAC Origen: Dirección MAC de 10.0.0.10 (nuestra estación)
✅ Protocolo: IPv4
❌ MAC Destino: ¡NO LA CONOCEMOS!

Problema: La estación de trabajo no sabe la dirección MAC de 10.0.0.20
Solución: Usar ARP (Protocolo de Resolución de Direcciones)

FASE 3: Solicitud ARP (ARP Request)
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

Si NO tienen esa IP → Descartan el mensaje
Si SÍ tienen esa IP → Responden


FASE 4: Respuesta ARP (ARP Reply)
Dispositivo 10.0.0.20 responde:
Trama ARP Reply:
[MAC Destino: MAC de 10.0.0.10] [MAC Origen: MAC de 10.0.0.20] [Protocolo: ARP] [La MAC para 10.0.0.20 es XX:XX:XX:XX:XX:XX]
Proceso:

10.0.0.20 sabe quién le preguntó (porque la MAC origen venía en la solicitud)
Crea una respuesta con su propia dirección MAC
Envía la respuesta directamente a 10.0.0.10 (no broadcast)


FASE 5: Envío del Ping Original
10.0.0.10 recibe la respuesta ARP:

Extrae la dirección MAC de 10.0.0.20
Completa la trama Ethernet del ping original:

Trama final del Ping:
[MAC Destino: MAC de 10.0.0.20] [MAC Origen: MAC de 10.0.0.10] [IPv4] [Paquete IP con ping]

✅ Envía el ping directamente a 10.0.0.20


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

Ejemplo de Caché ARP:
IP Address       MAC Address
10.0.0.20       AA:BB:CC:DD:EE:FF
10.0.0.30       11:22:33:44:55:66

Diferencias Importantes: Tabla ARP vs Tabla de Direcciones MAC
Tabla de Direcciones MAC (en Switches)

Ubicación: En switches (dispositivos Capa 2)
Mapeo: Puerto físico (Capa 1) → Dirección MAC (Capa 2)
Ejemplo: "Puerto 5 → MAC AA:BB:CC:DD:EE:FF"

Tabla ARP (en dispositivos con IP)

Ubicación: En computadoras, routers (dispositivos Capa 3)
Mapeo: Dirección IP (Capa 3) → Dirección MAC (Capa 2)
Ejemplo: "10.0.0.20 → MAC AA:BB:CC:DD:EE:FF"

⚠️ NO son la misma tabla aunque ambas contengan direcciones MAC

¿Por Qué No Usar Broadcast para Todo?
Pregunta del ejemplo: "¿Por qué no enviar todo a broadcast?"
Respuestas:

Ineficiencia: Todos los dispositivos recibirían todo el tráfico
Sobrecarga del switch: Se saturaría fácilmente
Anula el propósito del switch: Los switches están diseñados para crear conexiones directas
Pérdida de rendimiento: Cada dispositivo tendría que procesar paquetes que no son para él

ARP es la solución elegante:

Solo se usa broadcast una vez para descubrir
Después, toda comunicación es directa (unicast)


Diagrama del Flujo Completo
1. [10.0.0.10] Quiero hacer ping a 10.0.0.20
                ↓
2. No sé la MAC de 10.0.0.20
                ↓
3. [ARP Request BROADCAST] "¿Quién tiene 10.0.0.20?"
                ↓
4. [10.0.0.20] "¡Yo! Mi MAC es XX:XX:XX:XX:XX:XX"
                ↓
5. [10.0.0.10] Guarda en caché ARP
                ↓
6. [10.0.0.10] Envía PING directamente usando la MAC
                ↓
7. [10.0.0.20] Recibe ping y responde