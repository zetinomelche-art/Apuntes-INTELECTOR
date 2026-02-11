# Active Directory Domin Services
Es un protocolo que permite la resolucion de nombres de dominio, para usuarios y computadoras.

Esencial para AD DS que actua como mecanismo para de hubicacion de dominio para opperacion como autenticacion, actualizacions y busquedas.

- Tambien se usan para hubicarse entre si, en el caso de las replicas.

- El cliente consulta un servidor DNS para realizar tareas como:
      Detecta controladores de dominio.
      Convierte los nombres de equipo en direcciones IP.

## Ejemplo:
Cueando un usurio de red con una cunenta de AD inicia session en un dominio AD, el cliente consulta servidor DNS para buscar un controlador de dominio, despues el DNS responde con la IP de del controlador de dominio y comienza el proceso de autenticacion.

TCP (Protocolo de Control de Transmisión) 

En el caso de AD DS se implemta para facilitar la autentocacion y hubicacion del controlador de dominio 

Tambien se usa para hospedar zonas de busqueda publicas , lo que permite resolver nombres de direcciones IP o zonas de busqueda.

- DNS tambien permite utilizar las directivas DNS para equilibrar la carga de trafico entre distitas instancaias de una aplicacion

Administrar trafico segun hubicacion geografica, es decir usar directivas DNS para configurar que servers principales o secundarios respondan la consultas en funcion de la hubicacion geografica.

Filtrado, configrar directivas para crear filtros de consulta basados en parametros facilitados, es decir que responda de manera personalizada segun la peticion/consulta 

Análisis forense. Para redirigir a clientes no deseados a una IP inexistente

Redireccionamiento basado en la hora del día, es decir regirigir reducir el trafico, redirigiendolo a otras instancias de una app(desplegadas en otras hubicaciones) basadas en la hora del dia.

## Zona DNS
Una zona DNS es una parte del espacio de nombres DNS que administra un servidor DNS.
Dentro de una zona se guardan los registros DNS (como A, PTR, NS), y el servidor responde consultas sobre esos nombres.

Ejemplo:
La zona dominio.com contiene los registros necesarios para resolver nombres como www.dominio.com.

Se puden almacenar en un archivo local del servidor o en AD DS

## Tipos de zonas DNS

### Zona primaria

    Es la zona principal donde se crean, modifican o eliminan registros.

    Puede almacenarse:
    En un archivo local (.dns)
    En Active Directory (recomendado)

    Si está integrada en AD:
    Todos los DC con DNS pueden escribir en ella

    Se replica automáticamente entre controladores de dominio
    En Active Directory, todos los DC actúan como primarios.

### Zona secundaria
    Es una copia de solo lectura de la zona primaria.
    Obtiene la información mediante transferencias de zona.
    No se puede almacenar en Active Directory.

    Se usa para:
    Redundancia
    Compartir carga

### Zona de búsqueda inversa

    Permite resolver una IP a un nombre.
    Usa el dominio especial:

    in-addr.arpa

    Ejemplo:
    192.168.1.20 -> equipo.dominio.com

    Se usa principalmente para:
    Diagnóstico
    Seguridad
    Servicios de red

## Arquitectura DNS en Windows Server

DNS (Domain Name System) es un sistema que traduce nombres como www.contoso.com en direcciones IP, para que los equipos se puedan comunicar en la red.

## Organizacion de DNS
Dominio raíz -> .
Dominio de nivel superior (TLD) -> .com, .org, .edu
Dominio de segundo nivel -> contoso.com
Subdominios -> example.contoso.com
Host (equipo) -> pc01.example.contoso.com

Registros DNS (los más importantes)

## Los registros DNS guardan la información real:

### Registros A y AAAA (Address Records)
Función: Mapean nombres de dominio a direcciones IP
A (IPv4):

Asocia un nombre de host con una dirección IPv4 (32 bits)
Ejemplo: servidor.miempresa.com -> 192.168.1.10
Es el registro más común y fundamental
Un nombre puede tener múltiples registros A (round-robin para balanceo)

AAAA (IPv6):
Asocia un nombre de host con una dirección IPv6 (128 bits)
Ejemplo: servidor.miempresa.com -> 2001:0db8:85a3::8a2e:0370:7334
Mismo funcionamiento que A pero para IPv6


###  Registro CNAME (Canonical Name)
Función: Crea un alias o nombre alternativo para otro nombre de dominio
Características:

Apunta a otro nombre de dominio, NO a una IP directamente
Ejemplo: www.miempresa.com -> servidor.miempresa.com
Útil para tener múltiples nombres apuntando al mismo recurso
Restricción importante: No puede coexistir con otros registros del mismo nombre

Casos de uso:

ftp.miempresa.com -> servidor-archivos.miempresa.com
mail.miempresa.com -> exchange01.miempresa.com
Facilita cambios: solo actualizas el registro A del destino

### Registro MX (Mail Exchange)
Define los servidores de correo que reciben email para el dominio
Estructura:

Ejemplo: miempresa.com MX 10 mail1.miempresa.com
Ejemplo: miempresa.com MX 20 mail2.miempresa.com

### DNS e Internet

Los dominios de Internet son administrados por entidades oficiales.

Ejemplos de TLD:

.com -> empresas

.edu -> educación

.gov -> gobierno

.mil -> militar

.arpa -> DNS inverso

.sv, .us, .fr -> países

### UTF-8 en DNS(8-bit Unicode Transformation Format)
Unicode 8

Permite nombres con caracteres especiales
Internamente los convierte a minúsculas
Mantiene compatibilidad con servidores DNS antiguos


Politcas de grupos

Politica de grupo por defecto


# Ejemplo
Tengo un NAS y este no lo puedo unir al dominio, pero quiero que DNS sea capas de resolver sy direccion


ping -a 8.8.8.8(Para ver a que dominio pertenece la ip)