# DC

## Instalar el Rol AD DS

Abrir el Administrador del Servidor
    Clic en "Agregar roles y características"
        Siguiente → Siguiente
            Tipo de instalación: "Instalación basada en características o en roles"
                Selecciona tu servidor
                    En Roles del servidor, marca: "Servicios de dominio de Active Directory (AD DS)"
                        Se abrirá una ventana, clic en "Agregar características"
                            Siguiente → Siguiente → Siguiente
                                Clic en "Instalar"
                                    Espera a que termine la instalación (NO cierres aún)

Promover a Controlador de Dominio

1. En el Administrador del Servidor, verás una bandera amarilla con una notificación

2. Clic en la bandera -> "Promover este servidor a controlador de dominio"

3. Configuración de implementación:
    Seleccionar "Agregar un nuevo bosque"
    Nombre del dominio raíz: Ejemplo: tuempresa.local (elige el nombre de tu dominio)
    Siguiente

4. Opciones del controlador de dominio:
    Nivel funcional del bosque: Windows Server 2016 (o el más reciente disponible)
    Nivel funcional del dominio: Windows Server 2016
    Marca: Servidor DNS (debe estar marcado)
    Marca: Catálogo global (GC) (debe estar marcado)
    Contraseña DSRM: Ingresa una contraseña segura y anótala (para restauración del directorio)
    Siguiente

5. Opciones de DNS:
    Ignora la advertencia de delegación (es normal)
    Siguiente

6. Opciones adicionales:
    Nombre NetBIOS: Se genera automáticamente (Ejemplo: TUEMPRESA)
    Siguiente

7. Rutas de acceso:
    Deja las rutas predeterminadas (o cámbiala si tienes otra partición)
    Siguiente

8. Revisar opciones:
    Revisa la configuración
    Siguiente

9. Comprobación de requisitos previos:
    Espera a que termine la validación
    Ignora las advertencias de DNS (son normales en el primer DC)
    Clic en "Instalar"

10. El servidor se reiniciará automáticamente


# DC-RPL

# Instalar Rol AD DS como se hio antes

Promover como Controlador de Dominio Réplica

Clic en la bandera amarilla → "Promover este servidor a controlador de dominio"
Configuración de implementación:

Selecciona: "Agregar un controlador de dominio a un dominio existente" ⚠️ (NO crear nuevo bosque)
Dominio: tudominio.local (debería aparecer automáticamente)
Credenciales: Clic en "Cambiar"

Usuario: TUDOMINIO\Administrador
Contraseña del dominio


Siguiente


Opciones del controlador de dominio:

Nivel funcional del dominio: (aparecerá automáticamente según tu DC principal)
Marca: Servidor DNS ✅
Marca: Catálogo global (GC) ✅
Sitio: Default-First-Site-Name (o el que tengas)
Replicar desde: Selecciona tu DC principal o "Cualquier controlador de dominio"
Contraseña DSRM: Ingresa una contraseña segura (puede ser diferente al DC principal)
Siguiente


Opciones de DNS:

Marca: "Actualizar la delegación DNS" (si aparece)
Siguiente


Opciones adicionales:

Replicar desde: Debe aparecer tu DC principal (192.168.30.2)
Si no aparece, selecciona "Cualquier controlador de dominio"
Siguiente


Rutas de acceso:

Deja las rutas predeterminadas
Siguiente


Opciones de preparación:

Revisar opciones
Siguiente


Comprobación de requisitos previos:

Espera la validación
Puede aparecer advertencia: "No se pudo crear una delegación de DNS" → Es normal, ignórala
Puede aparecer: "Todos los registros SOA" → Normal
Clic en "Instalar"


El servidor se reiniciará automáticamente