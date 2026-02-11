# Hyper-V Network Virtualization (HNV)


Sirve para resolver problemas como, mover maquinas virtuales a la nube u otro datacenter sin tocar, IP, VLAN fisicas ni romper aplicaciones.

- Con HNV: la red se virtualiza, igual que las VMs

## Customer Address (CA) vs Provider Address (PA)

Este es EL concepto clave.

CA (Customer Address)
    - La IP que ve la VM
    - La IP “real” para el cliente
    - Ejemplo: 10.1.1.11

PA (Provider Address)
    - La IP que ve la red física
    - Solo existe en el datacenter
    - Ejemplo: 192.168.1.10

Analogía:

    CA = dirección escrita dentro de la carta
    PA = dirección escrita en el sobre

*La VM cree que vive en su red original, pero el datacenter la transporta usando otra IP*