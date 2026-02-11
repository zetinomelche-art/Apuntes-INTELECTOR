# Core Network Guide

Es lo minimo que necesita una empresa, para tener una red empresarial funcional con Windows Server

# Que es la red principal (Core Network)

Es la red principal, la cual es la base de toda la ingraestructura de TI.

Esta compuesta por:

    - Servidores
    - Protocolos de red
    - Servicios de autenticacion
    - Servicios de nombres

Todos estos elemtos forman la columna vertebral de la red.

# Componentes fundamentales para un Core Network

- TCP/IP
La base de la red, que permite que los dispositivos puedan comunicarse, tanto dentro de una red, como a internet.

- DHCP (Dinamyc Host Configuration Protocol)
Un servicio que permite que dispositivos en una misma red, obtengan una direccion IP, Gateway, Submascara de Red, DNS, de manera automatica.

- DNS
Permite resolver o traducir nombres de dominio a direcciones IP.
Active directori depende del DNS.

Ejemplo práctico

Supongamos:

Dominio: empresa.local
DC: DC01.empresa.local

Cliente arranca.

    - El cliente obtiene IP por DHCP
    - DHCP le dice cuál es el DNS
    - El cliente consulta DNS
    - DNS le dice dónde está el DC
    - El cliente usa Kerberos contra el DC
    - Inicio de sesión exitoso

- Active Directory (Cerebro)
El active directori permite la gestion de recursos de el servidor.
- Gestion de cuentas de usarios.
- Gestion de almacenamiento (QUOTAS)
- Gestion de equipos
- Politicas de grupo
- Autenticacion

    ## Concepto Clave, Bosque
        El bosque es el nivel mas alto, incluye uno o variso dominios, configuracion compartida, catalogo global, etc.
    
    ## Dominio Raiz del Bosque
        Es el primer dominio que se crea en el bosque, donde estan los administradores
    
    ## Base de datos centralizada
        Active directoru guarda todos los, equipos, usuarios, Grupos, Relaciones de Confianza en una base de datos central, esto permite autenticacion centralizada.



# Guia de Red Principal

Antes de implementar: ¿qué planear?

La guía recomienda planear lo siguiente antes de comenzar:
    - Planear subredes

Decidir rangos de direcciones, gateways y cómo se conectan las diferentes partes de la red.
    - Planear direcciones IP estáticas

Los servidores principales (DC, DNS, DHCP) deben tener direcciones fijas.
    - Convenciones de nombres

Definir cómo nombrar servidores para que sea consistente (ej. DC1, DHCP1).
    - Planear el dominio

Elegir:
Nombre del dominio
Nivel funcional del bosque (qué versiones de Server soportarás)
Pasos básicos para implementar
En general, la implementación se hace en este orden:
    - Configurar servidores físicos/virtuales
    - Instalar AD DS en DC principal (DC1)
    - Instalar DNS en el DC
    - Implementar DHCP
    - Unir servidores y clientes al dominio
    - Configurar servicios adicionales (NPS, IIS) si los necesitas
