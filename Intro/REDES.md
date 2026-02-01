# Que son las redes de datos
Son sistemas de hardare, software y proytocolos que se utilizan para tranportar informacion de un lugar a otro.

En sesncia las redes de datos lo que hacen es tomar un menasje, codificalo para ser enviado y lego el receptor lo decodifica


# MOdelo OSI (Open System Interconnect)(Interconexion de Sistemas Abiertos)
Creado en los anio 70. se uso para categorizar el orden en que los direfentes protocolos de red deben ejecutarses


## Capa 1 (Capa fisica)
Es la capa ficisica que utlizamos para conectarnos a la red, es decir cables de par trenzado, fibra optica, coaxilaes entre otros

## Capa 2 (CApa de enlace de datos)
Define los protocolos que se itlizan para la comunicacion.
Se usan diferentes protocolos para tranferiri los datos en  el caso de los dispositivos, pero todos funcionan al mismo nivel
wi-fi
ethernet
DOCSIS-3 es probable que se use para conectar el modem con el resto de internet

## Capa 3 (Capa de red)
EL doreccionamiento ip es el permite conectarse a casi cualquier dispositivos en internet


# Capa de  tranporte
Caoa encargada de establecer una session entre 2 puntos finales, cliente servidor
TCP la capa que encarga de configurar una session (TCP)  y crar una conexion y utlizala la capa de red paera encontrar lugar se encientra el dispositivos

## Capa de session no se usan
## Capa de presentacion
 
## CApa de aplicacion
HTTP, HTTPS(Hipertex tranfer protocol ), FTP, sFTP, 



# Ejemplo con las capas

7 Aplicacion layer
supongamos que tenenmos una app web, no la podemos mandar toda de golpe, por lo que tendremos dividirla en trozos

4 transpor layer
el trozo de antes lo pondremos en la capa de tranporte esta capa tiene encabezados como:
Source port | destination port | Flag (Que esta sucediendo) | payload(carga utul) es aqui donde se adjuntara el trozo de la app de la capa 7

3 Network layer
Src IP addres | Dest IP address | ttl |other | payload: aqui se adjunta toda la capa 4 

Toda la estructura antes vista se conoce como paquete

2 data link layer
Source MAC Addres | Destiantion Mac Address | Layer 3 protocol | payload aqui se adjunta nuestro paquete de la capa 4 (Maximun trasmition unir 1500bytes) 

esto se conoce como un marco, un fragmento de datos con un encabezado de data link layer, capa 3

1 una vez listo nuestro paquete podemos enviarlo por la capa fisica, donde se convertira a binarario y despues a pulsos electros.

# Otro ejemplo 
Aplication layer(7)| HTTP | HTTPs
Transport layer(4) | 80   | 443

TLS(Transport layer security)Seguridad de la capa de tranporte, porciona cifrado cuando se usa https  
FTP (Fole tranfer protocol)          |Port: 20/21
sFTP (Secure file tranfer protocol)  |Port: 22
TFTP (Trivial file tranfer protocol) |Port: 69
SMB (Server message block)           |Port: 445

En el caso de los Email hay 3 metodos que se ocupam

POP3 (Post office Protocol 3)   |Port: 110(Sin encriptar)/995(Encriptado)
Se utiliza para recuperar correos de un servidor a un cliente

IMAP (Internet Message Acces Protocol)  |Port: 143(Sin encriptar)/993(Encriptado)

SMTP (Simple Mail Transfer Protocol)    |Port: 25(Sin encriptar)/465(Encriptado)
Se utiliza para enviar un correo

# Autenticacion and DHCP
La mayoria de servicios de autenticacion no guardadn las credencianles normalmente, si no que lo hacen en el servidor, de esta manera se asegura que si inicia session en una maquinan doreferente siga teninento acceso a sus recursos y configuraciones asignadas  

LDAP    |Port: 389
LADPs   |Port: 636

DHCP (Dinamic HOst COnfiguration Protocol) |Port: 67/68
Encargado de proporcionaar una direccion IP a un dispositivo en la red, de manera automatica, es decir cuando se conecte que obtenga una IP

Contiene informacion como:

IP
Submascara de Red
Id de red
DNS

```bash
#Liberar la IP
ipconfig /release

#Recuperar IP
ipconfig /renew
```

# DNS (Domain NAme System)
DNS |Port: 53

Permite traducir nombres de dominio a direcciones IP 

1 se consulta cual es la de por ejemplo google.com
2 con esa direccion se contruye el paquete para emviarlo, como se vio en el ejemplo 1

```bash
#Ver hacia que IP esta resolviendo el host pluralsight.com
nslookup pluralsight.com
```

# NPT (Network Time Protocol)
NPT |POrt:123
Importante porque los servicios como el cifrado a menudo verifican si el server al que se conecta tiene un certificado valido y  dicho certificado es valido solo por un periodo de tiempo, ademas de otros servicios que necesitan de una hora precisa, por si ocurre algun evento separamos el momento exacto en que sucedio.

## UTC (Universsal Time Coordinate)
Esto es como se acomodan las diferentes zonas horarias 

# Network Management Protocols

## SSH
SSH |Port:22
Una utilidad que podemos utlizar para conectarnos a diferentes dispositivos, swtic, router, pc, etc

SSGing, son los dispositivos a los que nos conectamos

### SNMP (Simple Network Management Protocol)
Forma en las que los dispositivos envian info a un servidor, info como mensajes de reistro, info sobre activacion o desactivaxion de puertos u otro evento, los cientes que envian esta informacion son PC, router, etc

un server SNMP tambien pueden enviar un "Walk the tree", lo que significa que envien toda la informacion que tienen sobre los dispositivos que tiene asignado un numero SNMP, numeros llamados MIB(Management information BAse) y el server ocupa esta informacion para saber que esta sucediendo con los dispositicvos

## RDP (Remote Desktop Protocol)
Permite interactuar con nuestra interfaz grafica cuando no estamos en local, opera en el puerto 3389

## H.323
POrt: 1720, para video llamadas


## SIP (Protocol init session)
Port 5060/5061 para audio


SSS |Port:22


# SQL Database Protocols
 
mySQL       |Port:3306
SQLnet      |POrt:1521
SQL Server  |Port:1433


# Protocoles de la capa de transporte
Responsable de mantener y crear una session entre 2 puntos finales, genenralmente un cliente y un servidor 

## TCP(Transmision Control Protocol)

The 3-way Handsshake(Protocolo de enlace de 3 vias)
Es un proceso de configuracion muy preciso que el cliente y el servudor deben pasar para que podamos enviar informacion

1 el cliente envia un mensaje SYN que le indica al server que el cliente quiere comuniacarse

2 el servidor reponde con un mensaje llamado SYN-ACK esto indica al cliente que el server esta disponible

3 el cliente responde con un ACk o un reconocimienrto

una vez realizado este proceso el cliente puede por ejemplo solicitar un sitio web al server y el server responder con otro mensaje que contenga el sitio web

una vez terminada la tranferencia del sitio web el server respondera con un mensaje llamado FIN, una vez recibido por el cliente, el cliente respondera con un FIN-ACK y el mismo cleiten respondera con su propio mensaje de FIN y el server respondera con un FIN-ACK

RST(Restablecimiento TCP), se envia desde servidores y es como cortar la comunicacion, [uede provenir de un cleinte tambien o dispositivos intermedios.

## UDP (User datagram protocol)
Pide directamente la informacion al server y el server encvia, no exite un mecanismo para saver si se recibieron los datos o no

# Port Numbers 

## NUmeros de puerto del servidor
Denominados puertos conocidos y registrados

Conocidos
0-1023
HTTP 80
HTTPs 443
FTP 20 , 21
Telnet 23

Regsitrados
1024 - 49151 

## Numeros de puerto del cliente 
Denominoados puertos efimeros
Ephimereal
49152 - 65535


Los puertos efimeros o temporales se usan del lado del cliente el capa 4

# IPv4
Opera en la capa 3, capa de red, es un mecanosmo para que podamos comunicarnos largas distancias en internet.
Es un identificador unico para el dispositivo. Generalmente buscamos direcciones mediante el DNS

Una ip tine 2 cosas la porcion de red los primeros 3 octetos y el HOst Portion el ultimo octeto.

cada octeto esta conformado por 8bits


# Calses de IP
A -> 0.0.0.0    hasta   127.255.255.255
8 bits en la parte de la red y 24 en la parte de la subred

B ->128.0.0.0   hasta   191.255.255.255
16 bits en la parte de la red y 16 en la parte del host

C ->192.0.0.0   hasta   239.255.255.255 
24 bits en la parte de la red y 8 en la parte del host

D ->224.0.0.0   hasta   239.255.255.255 
32 bits en la parte de la red

E ->240.0.0.0   hasta   240.255.255.255

La primeras 3 clases se consideran clases de unidifucion y son que usamos en internet
La clase C de se usan para multidifusion y es cuando se tiene un serveer que enviar informacion sobre la res y hay muchos dispisitivos escuchando, ejemplo: RADIO FM

Las clas E son experimentales y no se usan


# Tipo de direcciones IP

Direccion de red
Un identificador para un grupo de dispositivos de red, tranbien llamado prefijo de red, similar a un codigo postal en la vida real

Broadcas Addres 
Permite a un remitente neviar un mensaje a todos los dispositivos

Host addred
La que se acupar aidentificar un dispositivo en la red


Ejemplo:

pAra la direccion de red, todos los ultimos binarios caen en 0
pAra la mascara de sbred todos los ulyimo ninarios caen en cero

para el broadcast todos los binarios caen en 1

10.128.224.64
00001010.10000000.11100000.010 00000
255.255.255.224
11111111.11111111.11111111.11100000

Con el ejemplo anterioro podemos ver que es una direccion de red, dado que los ultimos bits dictados por la mascara de subred estan en cero en la IP

# Direccion IP privadas
CIDR notacion (Classsles Inter-Domain Reouting)

Rango de Direcciomes IP Privadas
En 1994 se introdujo este concepto
La idea es que cualquier organizacion pueda usar la direcciones IP privadas y estas no se enrutaran publicamente en interner y permitiria implementar infraestrucuturas muy grandes sin entrar en conflicto con otras organizaciones


Private IP Addres Range
10.0.0.0/8 -> 10.255.255.255
172.16.0.0/12 -> 172.31.255.255
192.168.0.0/16 -> 192.168.255.255

RFC 1918 es el documento donde esto se define

APIPA
169.254.0.0/16

Ping (Package internet grouper)

Nerwork IP Addreds

Host IP Addresess

Broadcast IP Addresss

#
No se puede elejir una mascara de sub red arbitrariament, siempre hay verificar que no exista una superposicion

VLSM (Varible Length Subnet Masking)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~````

# IPv6
Nibble -> 4 bits
Byte -> 8 bits
Hextet -> 16 bits

En IPv6 se trabaja con secciones de 16 bist o un extet y se pude escribir con 4 valores hexadecimales con cada valor exadecimal de 4 bits


2a03:2880:f351:1:face:b00c:0:25de

Una ipv6 tiene una longitud de 128 bits y se escribe con 32 valores exadecimales y se separa en 8 hextetos y cada exteto se separa con 2 puntos

Em ipv6 generalmente se trabajara con una mascara /64(Bits) o tambien llamada porcion de red y la otra porcion de 64 sera el la porcion del host

Network potion     | Host portion o identificador de interfaz
2001:0DB8:0002:008D:0000:0000:00A5:52F5

## Trucos para simplificar in IPv6

1 - Quitar los ceros a la izquierda de cada hexteto
2001:0DB8:0002:008D:0000:0000:00A5:52F5 (Sin simplificar)
2001:DB8:2:8D:0:0:A5:52F5               (Simplificado)

1.1 Eliminar los ceros de los extetods que tengan ceros 
2001:DB8:2:8D:0:0:A5:52F5               (Sin simplificar)
2001:DB8:2:8D::A5:52F5                  (Simplificado)

Generalmente los orimeros 2 hextetos seran los mismos 2001:0BD8

NO se puede poner mas de 2 ::

# Doreccionamiento IPv6

-IPv6 Unicast Address (Direcciones de unidifusion IPv6)
Se utilizaon para pla comunicacion global es decir duispositicvos que no estqn en la misma red

Los dispositivos para comunicarse tendran 2 direcciones IP:
- Global unicast address
- IPv6 Link Local Address para la comunicacion local y siempre comenzara con FE80: y tendra una mascara /10 de forma predeterminada

Loopback address
equivalente a la 127.0.0.1 y sera ::1/128



Multicast Address
para la comunicacion de 1 a muchos

Anycast address 
Una direccion ip para muchos dispositivos
balancear cargas

Pila dual, es cuando pueden ejecutar IPv4 e IPv6 al mismo  tiempo

Winodws da priorirdad al IPv6 sobre el IPv4

# Obtener IPs cpn IPv6

## SLAAC Stateles Address Auto-Configuration (Autoconfiguracion de direcciones sin estado)
No existe en IPV4 

EL router enviarai periodicamente algo llamado Anuncio de enrrutador RA, lo que ara  es anuncioar en que sergmento de red esta

El equipo tomara esta direccion que le paso el router una /64 la otra parte de la IP en el xaso de windows la configurara automaticamente.

Creara 2 de estas direcciones antes mencionadas

Unix/Linux/Mac

Modified EUI - 64 
Lo que hara es tomar la direccion MAC del dispposititvos y al medio se le agregara FF:FE y esta hara que ya tengo una longitud de 64 bits dado que por defecto las direcciones MAC solo tienen 48 bits y en total quedara de 64 y se modifican un parde bits al inicio del primer hexteto y es asi como se obtiene la parte del host address.

## IPv6 DHCP (Dinamic Host Configuration Protocol)

OCnfiguraremos manualmente la red y cuando el host este listo para enviara un anuncio y y nuestro server DHCP respondera con una IP.
PAra configurar esto necesitamos desactivar SLAAC 


# Network Address  Traslation (NAT)
Una funcion de la capa de red capa 3

Ejemplo:
1 se intenta enviar una ,emsaje de la 10.0.0.10(Privada) a la  52.24.195.195(Publica), el mesaje de ida se enviaria correctamente
2 cunado la 52.24.195.195(Publica) intente responder hacia 10.0.0.10(Privada)  no podra hacerlo dado que y la descartara ddado que es una ip privada

Para evitar eso lo que el router hace es quitar la IP provada del paquete, guardarla en una tabla y despues reemplzar la ip que quito la ip del rouer que es una direccion IP publica y enrrutable.

Resumen: Reemplza las odrecciones ip de nuestros paquetes para que puedan acceder al internet publico

# DHCP (Dynamic Configuration Host Protocol)
Un protocolo de la capa de aplicacion

En una red domestica, el servidor DHCP esta integrado directamente en el router

DCHP scope (Alcamce)
Los parametros que se le asignaran al servidor DHCP
Network:    10.0.0.0/24
Excluded:   10.0.0.10 - 10.0.0.99
Gateway:    10.0.0.1
DNS:        8.8.8.8
Lease Time: 10,80 min

Gateway: Para que cuando intentemos enviar trafico fuera de nuestra red, nuestros clientes sepan como enrrutar ese traficao de manera adecuada

Flujo:

1 el clienen enviara un discover message
2 el servidor dhcp respondera con una oferta de IP DHCP-Offer, con toda la info antes presentada
3 el cliente responde aceptando la oferda DHCP

DHCP Binding (Vinvulante)
Lo que hace es en unta tabla vincular la direccion IP que entrego y la direccion MAC del dispositivo al que la entrego, ademas de el tiempo que se le entrega

En redes mas grandes se usara algo llamado IP Helper Address 
Esto para servidores DHCP que no estan en la misma sub red y funcioan de la sig Manera
1 se enviar el discover message a la IP helper address
2 El enrrutador determina y reeenviar el manseje a traves de la red a un server DHCP


# DNS (Domain Name System)(Domain Name Service)
Opera en la cap de tranporte (6)

URL(Uniform Resource Locater)

www.google.com

com -> Dominio de nivel Superior
google.com -> Dominio de segundo nivel
www.google.com -> Dominio de tercer nivel o hostname

Ejemplo: 
Al escribir www.dominio.com

1 primero de hara una bsuqueda DNS, y estosignifica enviar un mensaje desde el cleinte a un server DNS y preguntar por la direccion www.dominio.com y el server respondera con la direccion ip del dominio poor el que le estoy preguntando

2 ahora si el cliente puede armar un paquete para la IP que me respondieron

## Tipos de regsitro DNS

A -> orientado a IPv4
AAAA -> Orientado a IPv6
CNAME (Canonical Name) -> Utiliada si escribes por ejemplo gogle te rediril al dominio correccto
MX (Mail Exchage Record)
NS (Identifies Authoritative Name Server)
PTR (Pointer Record) -. Para la bsuqueda inversa
SRV (Service Rrecord)


DNS interno VS DNS Externo

Ejmeplo:

Si desde tu red internoa intestas llegar a ww.pluralsight.com, lo primero que se hara es consultar al server DNS interno, el server DNS interno no sabe como resolver este nombre de dominio por que redigira la solicitud a un server externo gcomo  el dns de google

Si el server dns de google no sabe como llegar lo que hara es consultaer el servidor del dominio Raiz en este caso .com y leugo el server raiz buscara el servidor de nombres autorizado y enviara la  respuesta a google.

Ahora el server de google ya sabe donde esta el servidor de bombre autorizado para pluralsight.com y le responde al dns de google

luego el dns de google repondera a nuestro server dns local y este lo guarda en chache para que la proxima vez que consulten no se vuelva repetir el proceso






# Topologias de RED

BUs Topology
Similar  tener nuestros equipos conectados al mismo cable, por ejemplo usar un cable coaxial para conectar todos nuestros dispositivos.
NO se usa desde finales de los 90

Ring Topologi
Conectar varios equipos como en anillo, se puede usar cables coaxiales, de par trenzado, etc


Topologia de estrella
Es kla que mas acupamos, donde hay un dispositivo central(un switch por ejemplo) y se extienden conexiones a cada dispositivo


# Blank Area Netwrks

## LAN WLAN

LAN (Local Area Network)
Multiples dispositivos conectados a un switch y esta conecion se ocupa en la capa 2

WLAN 
Multiples dispositivos conectados entre si mediante un dispositivo central, de manera inalambrica


## WAN (Wide Area Network) - Red de Area Amplia
Es donde tomamamos 2 LAN y los conectamos entre si, para conectarlas entre si necesitamos un router

## SAN (Storage Area Network) -Red de Area de Almacenamiento
Una SAN (Storage Area Network) es una red especializada de alta velocidad diseñada para conectar servidores con sistemas de almacenamiento

## CAN(Campus Area Network) y MAN(Metropolitan Area Network)
A menudo cuando hablamos de estos 2 terminos se refiere a una WAN donde se tiene muchas intalaciones conectada entre si

## PAN (Persnoal Area Network)
para conectar dispositivos a tu alrededor, por ejemplo, cuando te conectas a un smartwath


# WAN Tecnologies 

## Leased Line
- Copper (T1)
Se fue de las primeras y se usabara para pasar seniales de lineas analogicas a digitales, para que rocrrieran gran distancia sin perder calidad, no se usa tanto como antes

## Fibra Optica
Con capacidad de hasta 40Gbps, por lo que es una conexion de alta velocidad

-Dark Fiber
Se instala fibra optica en el suelo y esa fibra es oscura. Ademas que los clientes deben agregar sus propios laseres a esa fibra

-Metro Ethernet
Se utlizara la fibra para comunicacion paro el proveedor de internet ya tendra los laseres en la fibra, y proporcionara cierta infraestructura para que se conecte a la red.
Es posible controlar el hancho de banda

Multiprotocol Label Switching (Conmutación de etiquetas multiprotocolo), usaremos en la red de nuestro proveedor para que la red sea, segura, eficiente y confiable. 

Lo usariamo si tenemos 2 edificos demasiado lejos para conectarlos por cables de cobre

Software define WAN (SDWAN)

## Internet
- Satelite 
- Fibra  optica
- Calbe


## Conceptos

### T1 Link
-Bell Labs
-Hasta 1.544 Mbps

### T3
- hasta 44.736 Mbps

### ISDN

Primary Rate Interface (PRI)

# Virtualizaed NEtworks
Ha sucedido en datacenter desde el 2007. Antes de eso se utilizaba un servidor para un servidor especifico para cada tarea o incluso varias, por que mientras las tareas crecian la contidad de servidores apra ejecutarlsa tambien, por lo que en algun momento dejaria de ser escalable. Ademas que al hacer calculos se determini que solo se usaba solo el 10 a 15 porciento de la potencia de estos servidores.

Cuando se virtualizan servidores, se toma una parte del procesador, memoria, apra ejecutarlo, sin embargo necesitamos una forma de conectar estos dispositivos a la red, es qui donde se ejecuta la res red segura especial llamada VLAN, que es una forma de conectar nuestro servidores virtuales a la infraestructura de red fisica


# 3 tier network model (MOdelo de red de 3 niveles )
Se usa cuando se esta contruyendo redes, para proporcionar una res redundante, de alta velocidad y confiable.
Como organizamos el harware para mover el trafico


## Core
la clolumna vertebral de nuestra red
Conectara todos los nodos de la capa de distribucion.
MOvera rapidamente el trafico de una parte de la cap de distribuxion a otra

## Distribution
El encargado de conectar nuestro dispositivos de la capa de acceso y comenzar a construir una conexion entre, por ejemlo: las oficinas y centros de datos 
Se usaran dispositivos como switch, router para tomar los dispositivos de la capa acceso y conectarlo juntos.
Responsable de distribuir el acceso a la red a la capa de Acces
Filtrara el trafico

## Access 
Nuestra caoa de acceso es la manera en la que conectamos los equipos finales a un swtic.
El proposito es proporciones acceso a la red a los dispositivos
Controlar el acceso a la red
Cambios limitados


# Redes definidas por software

# Sotrage Area Network Connections (Conexiones de redes de are de almacenamiento)


# Software Defined Network (Redes definidas por software)
Por lo general se usan en datacenters y hay 3 capas


## Capa de  Aplicacion 
en las SDN la capa de aplicacion es donde los administradores pueden crear utilidaes y reglas que parmitan qye la red funcione de manera dinamica


POr ejemplo si hay una gran cantida de informacion proveniente de un dispositivo diferente, la cap de aplicaciom  puede tener politicas escritas para que se envien a la capa de conyrol  y esta las aplieu de manera que sea mas eficioente la red, y cunado este evento termine, volver a la configuracion anteriror




## Capa de  Control
La encargada de muchas de las cosAS QUE giran en torno a mover el trafico, como brindar la ip correcta dispositivos a traves del servicio DHCP.
Aplicar reglas de control de acceso para limitar a donde va el trafico


## Capa de Infraestrucutra
Consistira en routers, switchs que se diseniaran y conectaran juntos con ciertsas de politicas enrrutamiento.
Se puede usar esta capa solo para pasar el trafico

Redponsble de movel el trafico a la hubicacion correcta de la manera mas eficioente posible

### Management Plane
Un nuevo mecanismo de contro y seguimiento de todos los dispositivoa de nuestra red.

POdemos usaer este dispositivo para configurar algo llamado SDN(Red definida por software) o controlador DSN 

controlador DSN alojara toda la configuracion que se alicara, superpuesto al resto de nuestro hardware para falitiar el control y manipulacion de trafico


El comtrolador dsn enviara configuraciones adicionales a dispositivos de la capa de infraestructura



# SAN (Storage Area Network)
Necesitamos almacenar los datos de los server en algun lugar, es aqui donde entran los SAN

Hay 3 manerad e conectarnos a estos dispositivos

## fibre Channel

## Fibra channel over ethernet
En lugar de operar unicamente sobre conexiones de fibra optica, puede ejecutar sobre conexiones ethernet de alta velocidad

fibre Channel y Fibra channel over ethernet operan en la capa 2, la capa de enlace

## iSCI
Otro metodo que podemos ucupar para conectar nuestro SAN a nuestros servidores y usa el TCP/IP 


# SAAS PAAS IAAS

## SAAS (Software as a service)
Paquere offce
Google Office
Adobe

Hosted DNS (Alojamiento DNS)

## PAAS (Platform as a service)
Es donde se ofrece Hardware y software 
mayormente se usan del lado del servidor
Database

## IAAS (Ifraestructure as a service)
Es simplemente donde alquilamos una pieza de harware de servidor, por ejemplo alamcenamiento y es muy escalable.
Ofrece bastante automatixzacion


## (DAAS) Desktop as a service