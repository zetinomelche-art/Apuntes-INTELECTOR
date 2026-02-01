# Resumen: Work Folders (Carpetas de trabajo)

Work Folders es un servicio de rol de Windows Server que permite a los usuarios acceder y sincronizar sus archivos de trabajo desde distintos dispositivos, incluidos equipos personales (BYOD) y equipos corporativos, manteniendo el control centralizado de los datos por parte de la organización.

# ¿Qué es Work Folders?

Work Folders proporciona a los usuarios:

Un lugar único para almacenar archivos de trabajo.

Acceso a esos archivos desde cualquier lugar.

Sincronización automática cuando hay conexión a internet o a la red corporativa.

## Para la organización:

Los archivos se almacenan en servidores de archivos administrados.

Se pueden aplicar políticas de seguridad, como cifrado y contraseña de bloqueo de pantalla.

## Integración con soluciones existentes

Work Folders puede desplegarse junto con:

Redirección de carpetas

Archivos sin conexión

Carpetas personales (home folders)

Utiliza una carpeta del servidor llamada sync share, que puede contener datos existentes, permitiendo adoptar Work Folders sin migrar servidores ni datos.

## Usos comunes

Acceso a archivos de trabajo desde dispositivos personales y corporativos.

Trabajo sin conexión con sincronización posterior.

Uso conjunto con tecnologías existentes de archivos.

Administración mediante cuotas y clasificación de archivos.

Aplicación de políticas de seguridad en dispositivos.

Implementación con alta disponibilidad mediante Failover Clustering.

Características principales

Servicio de rol en Windows Server para crear y administrar sync shares.

Cmdlets de PowerShell para administración avanzada.

Integración nativa con Windows 10 y Windows 11.

Aplicaciones móviles para acceso desde otros dispositivos.

## Requisitos de software y infraestructura
Servidores y red

Windows Server 2012 R2 o superior.

Volúmenes formateados con NTFS.

Certificado de servidor confiable (preferiblemente de una CA pública).

Políticas de contraseña mediante Directiva de Grupo.

Opcionalmente, Active Directory con extensiones de esquema.

Requisitos para acceso desde Internet

Servidor publicado mediante un proxy inverso o gateway.

Dominio público con registros DNS.

Opcionalmente, infraestructura AD FS para autenticación.

# Requisitos del cliente

Windows 10 o Windows 11.

Espacio suficiente en un disco NTFS local.

Ubicación predeterminada: %USERPROFILE%\Work Folders.

Soporte para unidades USB o microSD NTFS.

Tamaño máximo por archivo: 10 GB.

Sin límite de almacenamiento por usuario (se puede controlar con cuotas FSRM).

Consideraciones importantes

No se admite la restauración de estados de máquinas virtuales cliente.

Las copias de seguridad deben realizarse desde el sistema operativo del cliente.

# Idea clave

Work Folders es una solución on-premises tipo “nube privada”, ideal para organizaciones que desean ofrecer acceso remoto y sincronización de archivos sin perder el control sobre la seguridad y la administración de los datos corporativos.
