# DC
Controador de dominio orincipal

## GPOs
    - A nivel de dominio
    - A nivel de OU
    - Habilitar la uditoria de incios de session (logIn, Logout, intentos fallidos)

## DNS
    Implemetar CNAME para FS-01 que se llame COMPARTIDOS

## Configuracion de RED
    - IP ->                   192.168.30.2
    - Submascarad de red ->   255.255.255.0
    - Gateway ->              192.168.30.1
    - 
    - DNS Preferido ->        192.168.30.2
    - DNS Alternativo ->      192.168.30.3



# DC-RPL
Controlador de dominio replica

## Configuracion de RED
    - IP ->                   192.168.30.3
    - Submascarad de red ->   255.255.255.0
    - Gateway ->              192.168.30.1
    - 
    - DNS Preferido ->        192.168.30.2
    - DNS Alternativo ->      192.168.30.3


# DHCP-Server
## Configuracion de RED del server DHCP
    - IP ->                   192.168.30.4
    - Submascarad de red ->   255.255.255.0
    - Gateway ->              192.168.30.1
    - 
    - DNS Preferido ->        192.168.30.2
    - DNS Alternativo ->      192.168.30.3


## Configuración del servicio DHCP
- Red                   -> 192.168.30.0/24
- Mascara de subred     -> 255.255.255.0
- Getway                ->  192.168.30.1

## DHCP (Scope)
- IPs para asignar(204)      -> 192.168.30.51 hasta 192.168.30.254
- IPs reservadas (50)  -> 192.168.30.1 hasta 192.168.30.50



# FS-01
Crear alamcenamiento por la red para el DC con iSCSI


        ## Dentro de un storage Pool en modo paridad crear: 
            - Captetas compartidas para los grupos de las OUs
            - QUOTAS para las carptes compartidad
            - Data deduplicacion
            - Filtrar archivos peligrosos .exe, .js, .bat, .ps1, etc
            - Habilitat auditoria mediante el visor de eventos de creacion eliminacion o actualizacion de archivos

## Configuracion de RED
    - IP ->                   192.168.30.5
    - Submascarad de red ->   255.255.255.0
    - Gateway ->              192.168.30.1
    - 
    - DNS Preferido ->        192.168.30.2
    - DNS Alternativo ->      192.168.30.3


# SMS-2019
Origen en 2019 preparado para migrar

## Configuracion de RED
    - IP ->                   192.168.30.6
    - Submascarad de red ->   255.255.255.0
    - Gateway ->              192.168.30.1
    - 
    - DNS Preferido ->        192.168.30.2
    - DNS Alternativo ->      192.168.30.3


# SMS-2025
Destino de la migracion

## Configuracion de RED
    - IP ->                   192.168.30.7
    - Submascarad de red ->   255.255.255.0
    - Gateway ->              192.168.30.1
    - 
    - DNS Preferido ->        192.168.30.2
    - DNS Alternativo ->      192.168.30.3



# Windows-10-0
Cleinte

la configuracion que deberia obtener:

IP ->                   192.168.30.51
Submascarad de red ->   255.255.255.0
Gateway ->              192.168.30.1

DNS Preferido ->        192.168.30.2
DNS Alternativo ->      192.168.30.3

# Windows-10-1
Cleinte

la configuracion que deberia obtener:

IP ->                   192.168.30.52
Submascarad de red ->   255.255.255.0
Gateway ->              192.168.30.1

DNS Preferido ->        192.168.30.2
DNS Alternativo ->      192.168.30.3



# Resumen
1. DC (192.168.30.2)          -> Instalar AD DS, promover a DC
2. DC-RPL (192.168.30.3)      -> DC réplica
3. DHCP-Server (192.168.30.4) -> DHCP, autorizar
4. FS-01 (192.168.30.5)       -> configurar iSCSI target, y storage spaces con SMB
5. SMS-2019/2025              -> Storage Migration service