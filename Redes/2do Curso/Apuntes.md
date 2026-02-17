# ¿Entre quiénes viajan las tramas Ethernet?

    - Las tramas Ethernet solo viajan dentro del mismo segmento de red (LAN), es decir:
    - Entre dispositivos directamente conectados entre sí
    - O conectados a través de switches
    - No cruzan redes diferentes por sí solas.

Otro ejemplo real: DHCP

Cuando conectas tu PC y no tiene IP:
Envía un mensaje DHCP Discover.

Lo envía en broadcast porque:
No sabe cuál es el servidor DHCP
No tiene IP configurada todavía

Entonces pregunta:
"¿Hay algún servidor DHCP aquí?"

Y el servidor responde.

En resumen

El broadcast se usa cuando:
    No sabes exactamente a quién enviarle el mensaje.
    Necesitas descubrir algo en la red.
    Estás iniciando comunicación (ARP, DHCP).


# Importante
Es un modo de comunicación donde los dispositivos pueden enviar y recibir datos

La trama ethernet define la estructura del datos que se envia, e informacion necesaria para ser interpretada
