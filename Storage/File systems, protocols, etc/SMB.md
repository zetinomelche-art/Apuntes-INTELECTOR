# Que es SMB
SMB (Server Message Block) es un protocolo de red utilizado para el uso compartido de archivos dentro de una red.
Permite realizar operaciones de crear, leer, actualizar y eliminar (CRUD) archivos, funcionando sobre la red TCP/IP.


# Usos

- Almacenamiento tradicional para datos de usuario final, lsa carpetas compartidas de windows en al red es un bien ejemplo

- En Hyper-V, los archivos de configuración y otros componentes de las máquinas virtuales pueden almacenarse en recursos de archivos compartidos, utilizando el protocolo SMB 3.0, lo que permite alta disponibilidad, mejor rendimiento y acceso remoto seguro.


# Caracteristicas

- Seguridad y autenticacion, proporciona, porciona algunas caracteristicas de proteccion como:   cifrado, firma, 

- Redes y conectividad: Adminte opciones de la capa de transporte como TCP, QUIC para acceso sin VPN

- Rendimiento, incluye caracterisiticas para mejorar el rendimiento en cuanto a la tranferencia de archivos


- Firma SMB, anterirormente solo necesaria para las captetas compartidas del controlador de dominio, SYSVOL y NETLOGON, partir de WSS 2025 y WS 11. Ahora esta de forma predeterminada

- Cifrado SMB de extremo a extremo, proporciona mayor seguridad.

- Limitar velocidad de autenticacion SMB, ayuda a porteger contra a ataques de fuerza bruta, disponible WSS 2025, WS11

- Auditoria de firma y cifrado SMB, activar la uditoria del servidor y cliente para admitir la dirma y cifrado SMB, si algun servidor o cliente no es compatible puede detectarlo 

- Acceso a cuentas de invitado deshabilitado, no permite el acceso a cuentas de invitado a un server remoto 

# Componentes de SMB

## Servidor SMB
Es quien comparte los recursos (archivos, impresoras, canalizaciones con nombre), y quien respondera y controlara solicitudes SMB

## Cliente SMB 
El que hace las solicitudes al server SMB y accedera a los recursos a traves de la red con la ruta UNC (Universal Naming Convention)



# Registro y auditoría de eventos
SMB permite a los administradores supervisar las actividades, para la auditoria, solucion o deteccion de prblemas, asi como la prevencion yu deteccion de amenazas.

Windows registra eventos SMB en el registro de eventos de Windows en Registros de aplicaciones y servicios > de Microsoft > Windows > SMBClient y SMBServer.

se regsitran los eventos de conectividad, seguridad, errores de autenticacion, acceso a recursos compartidos, etc.


## Configuración de puertos SMB alternativos
El cliente puede conectarse a puertos alternativos si elk  servidor esta comfigurado para hacerlo.

Tambien en posible bloquear esta configuracion, asi como configurar que servidores se conectan a que puertos

Compatible con WSS 2025 y WS11


Asignar un puerto alternativo

CMD 
```bash
# Para asignar un puerto TCP
NET USE <drive letter>: \\server\share /TCPPORT:<port number between 0 and 65536>

# puerto QUIC
NET USE <drive letter>: \\server\share /QUICPORT:<port number between 0 and 65536>
```



## Control de comportamiento de la firma

En caso de la firma estar deshabilitada en servidores o cleintes terceros aparecen lso sig errores:
```bash
0xc000a000
-1073700864
STATUS_INVALID_SIGNATURE
The cryptographic signature is invalid.
```
Para resolver esto, se debe habilitar la firma en el servidor de terceros


Al intentar conectarse a un dispositivo de terceros que tenga habilitadas la cuentas de terceros aparece el algunos de los sig. errores:
1. You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies help protect your PC from unsafe or malicious devices on the network.

2. Error code: 0x80070035
The network path was not found.

3. System error 3227320323 has occurred.

Deshabilitar la firma de SMB

### Deshabilitar la firma de SMB
en caso de necesitar conectar a un recurso y que en dicho server no exista la firma SMB o necesitar que las cuentas de invitado necesiten acceso, se ouede deshabilitar la firma a traves de la GPO o POwersehell

#### Deshabilitar por GPO

Seleccione Inicio, escriba gpedit.msc y presione Entrar.

En la ventana Editor de directivas de grupo locales, vaya a Configuración del equipo\Configuración de Windows\Configuración de seguridad\Directivas locales\Opciones de seguridad.

Abra Cliente de red de Microsoft: Firmar digitalmente las comunicaciones (siempre), seleccione Deshabilitado y luego elija Aceptar.


#### Deshabilitar por POwershell

Para deshabilitar la firma de SMB para conexiones salientes:
```bash
Set-SmbClientConfiguration -RequireSecuritySignature $false
```

Para deshabilitar la firma de SMB de las conexiones entrantes 
```bash
Set-SmbServerConfiguration -RequireSecuritySignature $false



```




### Habilitar la firma de SMB
La firma permite mantener la integridad de los datos mientras se transports, permite verificar la identidad del servidor y del cliente 

#### Hailitar la  firma SMB

POr GPO

Seleccione Inicio, escriba gpedit.msc y presione Entrar.

En la ventana Editor de directivas de grupo locales, vaya a Configuración del equipo\Configuración de Windows\Configuración de seguridad\Directivas locales\Opciones de seguridad.

Abra Cliente de red de Microsoft: Firmar digitalmente las comunicaciones (siempre), seleccione Habilitado y luego elija Aceptar.

Por powershell

Hablilitar la firma SMB de conexiones salientes:
Set-SmbClientConfiguration -RequireSecuritySignature $true

Habilitar la firma del servidor SMB de conexiones entrantes:
Set-SmbServerConfiguration -RequireSecuritySignature $true

Verificar el estado de firma de SMB


## Verificar el estado de firma de SMB
Saliente
Get-SmbClientConfiguration | FL RequireSecuritySignature

Emtrante
Get-SmbServerConfiguration | FL RequireSecuritySignature



# limitador de velocidad de autenticación SMB
w11 necesario

Creado para evitar ataques de fuerza bruta, SMB usa el delimitador de autenticacion para que sea cada 2 segundos (Predeterminado)

Para habilitarlo con powershell
```bash
Set-SmbServerConfiguration -InvalidAuthenticationDelayTimeInMs <Milliseconds>
```
ver el valor actual
```bash
Get-SmbServerConfiguration | Format-List -Property InvalidAuthenticationDelayTimeInMs
```


# Configuración del cliente SMB para requerir cifrado en Windows

Se puede configurar el cliente para que requiera cifrado en todas las conexiones salientes

Cuando se habilite el cliente no permitira conexiones que no esten cifradas 

Proporciona seguradad contra ataques de interceptacion

Unicamente disonible para WS11 o posteriror 

## COnfiguraicion de mandato de cifrado mediante GPO y powershell
w11 necesario

Mediante GPO:

Abra la Consola de administración de directivas de grupo.
Edite o cree un objeto de directiva de grupo (GPO) que quiera usar.
En el árbol de la consola, seleccione Configuración del equipo > Plantillas administrativas > Red > Estación de trabajo Lanman.
Para la configuración, haga clic con el botón derecho en Requerir cifrado y seleccione Editar.
Seleccione Habilitar y seleccione Aceptar.

Mediante POwerShell
Set-SmbClientConfiguration -RequireEncryption $true

Ver la configuracion en una maquina:
Get-SmbClientConfiguration | Format-List -Property RequireEncryption


# Protejer el acceso SMB
Bloquear el acceso mediante el puerto 445 evititando el acceso desde internet

# Deshabilitar el servidor SMB si no se usa


# Habilitar los inicios de sesión de invitado no seguros.
La habilitación de inicios de sesión de invitado puede ser necesaria cuando un usuario necesita acceder a un recurso en un servidor, pero el servidor no proporciona cuentas de usuario, solo acceso de invitado.

# Compresion
ws11 necesario en el cliente


Intentar siempre la compresión (cliente SMB)

Ejecute la Consola de administración de directivas de grupo para el dominio de Active Directory y cree o vaya a una directiva de grupo.
Expanda la directiva Computer Configuration\Policies\Administrative Templates\Network\Lanman Workstation.
Habilite la directiva Use SMB Compression by Default.
Cierre el editor de directivas.


Intento de compresión siempre (servidor SMB)

Ejecute la Consola de administración de directivas de grupo para el dominio de Active Directory y cree o vaya a una directiva de grupo.
Expanda la directiva Computer Configuration\Policies\Administrative Templates\Network\Lanman Server.
Habilite la directiva Request traffic compression for all shares.
Cierre el editor de directivas.


# SMB Directo
admite el uso de adaptadores de red que tienen capacidad de acceso directo a memoria remota (RDMA).
Para servicios como Hiper-V o SQL-server permite que el almacenamiento SMB se paresca al almacenamiento local