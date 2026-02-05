# Storage Space Direct

Es una tecnologia de microsoft que permite convertir varios discos internos de varios servidores en un solo almacenamiento compartido.

Sin SAN, o fiber channel

# Sirve para
Crear alamcenamiento definido por software, el hardaware de servidores normales

El alamcenamiento
- Se replica
- Se protege
- Se acelera
- Se repara solo

Todo por software


# Se necesitan 

- 2 servidores
- 16 maximo

cada server con sus discos locales

# Idea clave

SRV-0 -> 4 discos
SRV-1 -> 4 discos
SRV-3 -> 4 discos
    
- Con storage space direct todos estos discos van a un solo pool, si un disco o server muere, los datos aun siguen ahi

# Que hace automaticamente
- Detecta los discos nuevos
- Usa SSD/NVMe como chache
- Replica datos
- Se auto-repara si algo falla

# Tecnologias de windows que combina

SMB 3 -> Comunicación rápida entre servidores
Storages Spaces -> RAID por software
ReFS -> Sistema de archivos moderno, con gran capacidad para autorepararse y soportando miles de teras


# Beneficios reales
- Buen rendimiento
- Tolerancia a fallos
- Escalabilidad

# Importante
- Existen 2 alternativas de proteccion

- Mirror  -> Copias exactas de los datos  -> Rapido y seguro
    - Tolera 1 fallo
    - Eficiencia al 50%

- 3 copias (3 way mirror) 
    - 3 copias
    - Tolera 2 fallos
    - Eficiencia al 33.33%
    - Minimo de 3 servidores

- Paridad -> Datos y calculos matematicos -> Eficiente con el alamcenamiento
    - más CPU y más lento

- Dual parity (RAID 6 moderno)
    - Tolera: 2 fallos
    - Mínimo: 4 servidores
    - Eficiencia: 50% -> 80% (depende del tamaño)


# Understanding the Storage Pool Cache
Windows usa los discos más rápidos para acelerar a los más lentos, sin que tú tengas que hacer nada.

Tipos de discos qe acpeta
    - PMem (memoria persistente)
    - NVMe
    - SSD (SATA/SAS)
    - HDD

## Tipos de despliegue
- All-flash 
    Solo NVMe y/o SSD

- Hybrid
    SSD o NVMe + HDD