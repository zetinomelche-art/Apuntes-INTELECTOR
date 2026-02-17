# Storage Migration Service

# Que es?
Una herramientoa de microsoft que sirve para migrar o mover archivos y servidores de archios viejos a servdiores nuevos, maquinas virtuales o Azure, sin que los usuarios noten nada

# Se usa cuando
- Se tiene hardware muy viejo que ya no cumple con los estandares
- Migrar servidores antiguos
- Para migrar a la nube Azure por ejemplo

# Storage migration Service Permite
 
## Inventariar Servidores
- Ve que archivos hay
- que carpetsa compartidas existen
- Permisos

## Capiar datos
- Archivos, carpetas, Permisos NTFS y de recuros compartidos

## Trancision de identidad
El server nuevo toma nombre e IP del viejo 


# Como funcioan la migracion

1 - Inventario
Se escanean los servidores o servidor de origen para saber que archivos y configuracion existen y que se va a migrar

2 - Transferencia
Se copian los datos del sever viejo al nuevo
El server viejo sigue funcionando

3- Trancision
El Server nuevo puede tomar la identidad del viejo, ip, nombre, recursos compartidos.
El server viejo entra en mantenimiento
Ya no acept conexiones
Aun tiene los datos


# Componentes necesarios

1 - Servidor origen

2 - Servidor destino

3 - Servidor orquestador 
Este coordina, copia y maneja la trancision

- Si es un solo servidor destino puede ser el orquestador

-- Todos los server deben estar en el mismo dominio
-- En server controladores de dominio no se puede hacer trancision pero si copiar archivos

# Que si conserva

Datos

    - Archivos y carpetas
    - Estructura completa de directorios
    - Fechas (creación, modificación, acceso)
    - Atributos (solo lectura, oculto, etc.)

🔐 Seguridad

    - Permisos NTFS
    - Propietarios de archivos
    - Herencia de permisos
    - Auditoría NTFS

🌐 Comparticiones de red (Shares)

    - Nombres de los shares
    - Permisos de compartición
    - Paths originales
    - Configuración SMB

🧑‍🤝‍🧑 Identidad

    - Funciona con cuentas locales y de dominio
    - Mantiene SIDs (muy importante)

🧭 Red (opcional en Cutover)

    - IP Address
    - Nombre del servidor
    - Pertenece al dominio (si eliges cutover)

🔁 Sincronización

    - Permite varias sincronizaciones antes del corte final
    - Solo copia cambios (delta)

QUÉ NO CONSERVA (NO migra)
Aplicaciones

    - Programas instalados
    - Servicios de terceros
    - Roles no relacionados con archivos

🚫 Sistema

    - Sistema operativo
    - Registro completo de Windows
    - Drivers
    - Configuraciones personalizadas del SO

🚫 Roles NO compatibles

    - DHCP
    - DNS
    - Active Directory
    - IIS
    - Print Server (solo archivos, no colas)

🚫 Configuración avanzada SMB

    - SMB Multichannel
    - SMB Direct (RDMA)
    - Quotas de FSRM (se recrean manualmente)

🚫 Tareas y scripts

    - Scheduled Tasks
    - Scripts personalizados
    - GPO locales

