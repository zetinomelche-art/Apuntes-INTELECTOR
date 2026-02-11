# Hyper-V Virtual Switch

Permite crear un Swicth Virtual de Capa 2, que conecta maquinas virtuales entre si y con la red fisica

# Sirve para 

    - La red interna del host
    - La red de la empresa (LAN)
    - Internet
    - Redes virtuales (Software-Defined Networking)

# Tipos de Hyper-V Virtual Switch

External
    - Conecta VMs a la red física
    - Permite acceso a LAN e Internet

Internal
    - Comunicación entre VMs y el host
    - No sale a la red física

Private
    - Solo comunicación entre VMs
    - El host no participa

# Seguridad integrada

## ARP / ND Spoofing Protection

Evita que una VM:
    - “robe” la IP de otra
    - Haga ataques MITM(Man in the middle)

DHCP Guard
    - Evita que una VM se haga pasar por servidor DHCP falso

# Control de ancho de banda

    - Garantizar ancho de banda mínimo
    - Limitar ancho de banda máximo
    - Permitir burst (picos)

# Protección contra VMs maliciosas

    - Monitoreo de tráfico
    - Inspección de paquetes
    - Diagnósticos
    - Eventos en logs

    - Ideal para
        ' Datacenters
        ' Hosting
        ' Laboratorios empresariales

        