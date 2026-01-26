# Teoria
GPO local Cada equipo con alguna versión actual de Windows tiene unGPO almacenado localmente. Para crear un GPO local, use el Editor de directivas de grupo

GPO de sitio. Se aplica a todos los dominios del sitio. Los sitios pueden te-ner vinculados uno o más objetos GPO y se aplican en el orden establecido.

GPO de dominio. Se aplica dominio por dominio; un dominio hijo no he-reda las directivas del dominio padre. Los dominios pueden tener vincula-dos uno o más objetos GPO y se aplican en el orden establecido.

GPO  de  unidad  organizativa. Se aplican a las unidades organizativas;una unidad organizativa secundaria hereda las directivas de la unidad or-ganizativa primaria. Los objetos GPO vinculados a las unidades organiza-tivas se aplican siguiendo la jerarquía de ellas.


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