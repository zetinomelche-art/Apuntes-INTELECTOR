# Teoria
GPO local Cada equipo con alguna versión actual de Windows tiene unGPO almacenado localmente. Para crear un GPO local, use el Editor de directivas de grupo

GPO de sitio. Se aplica a todos los dominios del sitio. Los sitios pueden te-ner vinculados uno o más objetos GPO y se aplican en el orden establecido.

GPO de dominio. Se aplica dominio por dominio; un dominio hijo no he-reda las directivas del dominio padre. Los dominios pueden tener vincula-dos uno o más objetos GPO y se aplican en el orden establecido.

GPO  de  unidad  organizativa. Se aplican a las unidades organizativas;una unidad organizativa secundaria hereda las directivas de la unidad or-ganizativa primaria. Los objetos GPO vinculados a las unidades organiza-tivas se aplican siguiendo la jerarquía de ellas.

# Politicas por defecto

Default Domain Policy

La política que controla la seguridad de cuentas de usuario a nivel de TODO el dominio.
Se aplica a:

Todos los usuarios y equipos del dominio

Configuraciones principales:
Políticas de Contraseñas:

Longitud mínima (7 caracteres por defecto)
Complejidad requerida (mayúsculas, minúsculas, números, símbolos)
Expiración (42 días por defecto)
Historial de contraseñas (24 recordadas)


# Default Domain Controllers Policy

La política que protege y asegura los servidores Domain Controllers (los más críticos del dominio).
Se aplica a:

Solo los Domain Controllers (servidores en la OU "Domain Controllers")

Configuraciones principales:
Derechos de Usuario:

Quién puede iniciar sesión localmente en los DCs
Quién puede acceder por Remote Desktop
Quién puede hacer backups y restauraciones
Quién puede cambiar la hora del sistema

Auditoría:

Registrar inicios de sesión exitosos y fallidos
Registrar cambios en cuentas de usuario
Registrar cambios en Active Directory
Registrar cambios en políticas



# Bloquear panel de control
User Configuration
    Administrative Templates
        Control Panel

Buscar la política Prohibit access to Control Panel and PC settings

Hacer doble clic sobre ella

Marca la opción Enabled

Presiona Apply

Luego OK


# Fondo de pantalla predeterminado e impedir que lo cambie

Clic derecho -> Create a GPO in this domain, and Link it here

User Configuration
    Policies
        Administrative Templates
            Desktop
                Desktop

Abre Desktop Wallpaper

Marca Enabled

En Wallpaper Name, escribe la ruta UNC:
\\SERVIDOR\Wallpapers\fondo_empresa.jpg

En este caso para la replica, crear una carpeta de wallpapers en la ruta C:\Windows\SYSVOL\domain\scripts aho crear una nueva captea y poner la wallparer
C:\Windows\SYSVOL\domain\scripts\wallpaper\fondo.jpg

en la ruta del fondo ponemos
\\dominio.com\SYSVOL\dominio.com\scripts\Wallpapers\fondo_empresa.jpg



## Impedir que cambie el fondo de pantalla
User Configuration
    Policies        
        Administrative Templates
            Control Panel
                Personalization

Abre Prevent changing desktop background
Marca Enabled
Aplica y acepta


# ABloqueae el regedit
User Configuration 
    > Administrative Templates 
        > System 
            > Prevent access to registry editing tools


# Desplegar una app con GPOs con un .msi

## Crear carpeta compartida
C:\GPO-Software
Dentro copiar el .msi de la App
Comparte la carpeta:

Clic derecho > Propiedades

Compartir > Uso compartido avanzado
            > Marcar Compartir esta carpeta
            > Nombre: Por defecto
            > Permisos
                > Agregar Domain Computers o person a ogrupo a compartir
            > Permiso: Lectura
          > Pestania Security
                > Seleccionar el grupo o persona a compartir y asignar permisos de ejecucion

Ingresando desde un equipo cliente deberia verse asi:
\\Server-Nombre\Carpeta-compartida\archivo.msi

## Configuracion de la GPO

> Navegar hasta la UO donde se desea implementar la politica

> Crear una nueva GPO

> Clic derecho sobre la GPO 
    > Editar
        > Comfiguracion de usuario o Configuración del equipo
            > Directivas
                > Configuración de software
                    > Instalación de software

En Instalacion de Software
Clic derecho 
    > Nuevo
        > Paquete
        Buscar usando la ruta UNC:
        \\Server-Nombre\Carpeta-compartida\archivo.msi
        
        Tipo de implementación:
        Asignado

## Importante!!!
Clci derecho sobre el paquete
    > Propiedades
        > Deployment
            > Instalar en el proximo inicio de session


# Abilitar la auditoria de incios de session

Editar la politica:
Default Domain Controllers Policity
    > Computer configuration
        > Policies
            > Windows setings
                > Security settings
                    > Advanced Audit Policy Configuration
                        > Logon/Logoff
                            > Audit Policies
                                > Audit Logoff
                                    Propiedades:
                                    Success and Failure
                                > Audit Logon
                                    Propiedades:
                                    Success and Failure
                                > Audit Other Logon/Logoff Events
                                    Propiedades:
                                    Success and Failure

gpupdate /force

## Algunos IDs
Inicio de Sesión:
Event ID: 4624
    Descripción: Se registra cuando un usuario inicia sesión correctamente en el sistema.
Inicio de Sesión Fallido:
    Event ID: 4625
    Descripción: Se registra cuando hay un intento de inicio de sesión que no tiene éxito, ya sea debido a un nombre de usuario o contraseña incorrectos.
Cierre de Sesión:
    Event ID: 4634
    Descripción: Se registra cuando un usuario cierra sesión en el sistema.
