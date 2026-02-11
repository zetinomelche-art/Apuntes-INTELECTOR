# IPAM (IP Address Management )

IP Address Management (IPAM) es una herramienta de Windows Server que permite:

    - Planificar direcciones IP
    - Implementar infraestructura IP
    - Administrar DNS y DHCP
    - Monitorear servidores de red
    - Llevar inventario de direcciones IP

En pocas palabras:

IPAM es un centro de control para administrar direcciones IP, DNS y DHCP desde un solo lugar.



## Cuando se instala

- Descubre servidores DHCP y DNS en la red.
- Recoge información cada 6 horas.
- Guarda los datos en una base de datos local.
- Muestra notificaciones sobre cuándo se actualizó la información.


## Administración de IPAM
¿Qué permite administrar?

    Gestionar zonas DNS
    Gestionar registros DNS
    Administrar DHCP
    Aplicar control de acceso por roles (RBAC)
    Auditar cambios (registro de modificaciones)


## IPAM y la Gestión de Registros DNS
¿Qué recoge IPAM de DNS?

IPAM recopila:
    - Zonas DNS
    - Registros DNS
    - Información de zonas directas y reversas
    - Registros A, AAAA, MX, CNAME, PTR, SRV, etc.

Ejemplos de registros que puede manejar:

    - A / AAAA (direcciones IP)
    - CNAME (alias)
    - MX (correo)
    - PTR (reverse lookup)
    - SRV (servicios)
    - TXT
    - SOA
    - NS

## Qué integración hace IPAM?

IPAM conecta todo:
    - IP Address Inventory + DNS Zones + DNS Records
    - Crea inventario de IP desde registros A y AAAA
    - Relaciona rangos IP con zonas reversas
    - Crea automáticamente IPs para registros PTR