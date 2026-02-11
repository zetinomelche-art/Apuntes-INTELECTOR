# Dynamic Host Configuration Protocol

Es el encargado de proporcionar confuguracion de red de manera dinamica a dispositivos clientes.

Asigna automáticamente direcciones IP y configuración de red a los dispositivos.

Sin DHCP, tendrías que configurar manualmente en cada PC:
    - Dirección IP
    - Máscara de subred
    - Gateway
    - DNS - 

# Como funciona DHCP

Cuando una PC se conecta a la red:

Paso 1 – DHCP Discover

    - El cliente dice:
    “¿Hay algún servidor DHCP por aquí?”

Paso 2 – DHCP Offer

    - El servidor responde:
    “Sí, aquí tienes esta IP: 192.168.1.25”

Paso 3 – DHCP Request

    - El cliente dice:

    “Acepto esa IP”

Paso 4 – DHCP Acknowledge (ACK)

    El servidor confirma:
    - “Perfecto, puedes usarla por 8 horas”

A esto se le llama:

Proceso DORA (Discover, Offer, Request, Acknowledge)

# Informacion que se entrega al cliente

    - IP
    - Máscara de subred
    - Puerta de enlace (Default Gateway)
    - Servidores DNS
    - Nombre de dominio DNS

Otras opciones avanzadas

Estas configuraciones adicionales se llaman:
DHCP Options
Ejemplo importante:
Opción 003 → Router
Opción 006 → DNS Servers

# Informacion que conserva el server DHCP

- Pool de direcciones

Rango de IP disponibles
Ejemplo:
192.168.1.100 – 192.168.1.200

-Exclusiones

    IP que NO deben asignarse

- Reservas
    Una IP fija para una MAC específica
    Ejemplo:
    La impresora siempre recibe 192.168.1.50

- Duración de concesión (Lease)
    Tiempo que el cliente puede usar la IP

# Características avanzadas en Windows Server

## DHCP Authorization (Muy importante en dominio)

Solo los servidores DHCP autorizados pueden asignar IP.
Rogue DHCP Servers (servidores no autorizados)

## DHCP Failover

Permite tener 2 servidores DHCP compartiendo el mismo scope.

Beneficios:
    - Alta disponibilidad
    - Balanceo de carga
    - Si uno cae, el otro sigue funcionando
    - Muy usado en empresas.

## DHCP Policies

Puedes crear reglas como:

Si la MAC es X → asignar IP específica
Si es cierto tipo de dispositivo → dar configuración diferente

## DHCP Audit Logging

Registra:

    - Quién recibió IP
    - Cuándo se renovó
    - Errores
    - Útil para troubleshooting.

## Integración con DNS

Cuando DHCP asigna una IP:

Puede actualizar automáticamente el registro DNS.

Ejemplo:
    - PC01 recibe 192.168.1.50
    - DNS se actualiza automáticamente.
Esto es crítico para Active Directory.

## IPv4 e IPv6

DHCP soporta ambos protocolos.
