# Brancache

Es una tecnologia para ahorrar ancho de banda en un WAN, guardadndo copias locales de contenido que viene desde la nube u oficina central, para que no se descarge una y otra vez el mismo contenido

## El escenario típico donde se usa

Empresas con:


    - Oficina central (HQ)Varias sucursales (branch offices)
    - Conexión entre sedes por WAN lenta o costosa
    - Archivos, web o apps están en:
    - File servers
    - IIS
    - Apps BITS
    - Cloud

# Como funciona

Cliente en sucursal pide un archivo

## El servidor central:

    - Verifica permisos
    - Envía metadatos (hashes), no el archivo completo

## El cliente:

    - Busca si el contenido ya existe en la sucursal

## Si existe:

    - Lo descarga localmente

## Si no existe:

    - Lo baja por WAN
    - Lo guarda en cache para los demás

# Modos de brancache

## Distributed Cache Mode

Cada cliente guarda cache, los clientes se comparten contenido entre sí

Ideal para:
    - Sucursales pequeñas
    - Sin servidor local

Limitaciones:
    - Funciona solo en un subnet
    - Si el cliente que tiene el archivo se apaga -> adiós cache
    - Clientes con Windows distintos no siempre comparten cache

## Hosted Cache Mode

Hay un servidor local que guarda todo el cache, los clientes siempre van a ese servidor

Ideal para:
    - Sucursales medianas o grandes
    - Varias subredes
    - Alta disponibilidad

Ventajas clave:

    - Cache siempre disponible
    - Mejor ahorro de WAN
    - Centralizado
    - Compatible con múltiples subnets

# Quines pueden usar branchache

File Servers

SMB
    Requiere:
    - Rol File Services
    - BranchCache for Network Files
    - Hash generation habilitada

Web Servers

# Seguridad de BranchCache
Usa:

    SHA-256
    HMAC
    AES-128

El cache:

    - Está cifrado (en versiones modernas)
    - Se valida por hashes

Nadie puede:

    - Modificar contenido sin que se detecte
    - Leer cache sin permisos


# S un archivo cambia

El usuario guarda cambios -> van directo al servidor central

BranchCache:
    -No interfiere
    -No rompe versiones

El siguiente usuario:
    - Solo descarga los bloques nuevos