# Network Load Balancing

Hacer que varios servidores se vean como un solo servidor lógico para los clientes.

Desde afuera:
    Un solo nombre
    Una sola IP (VIP)

Por dentro:
    2 o más servidores reales atendiendo las solicitudes

# Para que sirve Network Load Balancing

Sirve para alta disponibilidad y escalabilidad de servicios de red, como:
    - Web (IIS)
    - FTP
    - VPN
    - Firewall / Proxy

Otros servicios críticos basados en TCP/IP

# Importante

NLB crea un clúster virtual:
    - No hay almacenamiento compartido
    - No hay nodo maestro
    - Todos los servidores están activos
Cada servidor del clúster se llama host.
Todos los hosts:
    - Tienen su IP propia (dedicada)
    - Comparten una IP virtual (Cluster IP o VIP)


## Como se distribuye el trafico

- NLB funciona en red, no en la aplicación.
- Usa TCP/IP
- Decide qué host atiende cada conexión
- El cliente no sabe a qué servidor real llega

Puedes:
    - Repartir carga equitativamente
    - Dar más carga a un host específico
    - Mandar todo a un solo host (default host)


## Que pasa si un server falla

Aquí entra la alta disponibilidad:
    - NLB detecta el fallo
    - Redistribuye la carga automáticamente
    - Ocurre en ~10 segundos
    - El servicio sigue funcionando

Cuando el host vuelve:
    Se reintegra solo
    Recupera su parte de carga
    Casi transparente para el usuario.

# Escalanilidad

NLB permite crecer fácilmente:
Hasta 32 servidores por clúster
Agregar hosts sin apagar el servicio
Quitar hosts cuando baja la carga


# Administración (Manageability)

Puedes administrar NLB con:

    - Network Load Balancing Manager
    - PowerShell
    - Windows Admin Center

Funciones importantes:

Reglas por puerto (port rules)
Reglas por aplicación
Bloqueo de puertos
Envío de tráfico a host específico
Control remoto del clúster