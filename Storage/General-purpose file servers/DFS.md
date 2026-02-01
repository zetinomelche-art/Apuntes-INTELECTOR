# Distributed File System

Los Espacios de nombres DFS son un servicio de rol de Windows Server que permiten unificar carpetas compartidas ubicadas en distintos servidores dentro de una estructura lógica única.

Para el usuario, esto se traduce en una ruta de acceso virtual única, aunque los archivos reales estén almacenados en diferentes servidores. El acceso es transparente y no requiere que el usuario sepa en qué servidor se encuentra el contenido.


# Instalación de espacios de nombres DFS

Abra el Administrador del servidor, haga clic en Administrar y, a continuación, en Agregar roles y características. Aparece el Asistente para agregar roles y características.

En la página Selección de servidor, seleccione el servidor o el disco duro virtual (VHD) de una máquina virtual sin conexión en la que desee instalar DFS.

Seleccione los servicios de rol y las características que desee instalar.

Para instalar el servicio Espacios de nombres DFS, en la página Roles de servidor, seleccione Espacios de nombres DFS.

Para instalar solamente las Herramientas de administración de DFS, en la página Características , expanda Herramientas de administración remota del servidor, Herramientas de administración de roles, expanda Herramientas de Servicios de archivo y, a continuación, seleccione Herramientas de administración de DFS.

DFS Management Tools instala el complemento Administración DFS, el módulo Espacios de nombres DFS para Windows PowerShell y las herramientas de línea de comandos, pero no instala ningún servicio DFS en el servidor.

# Administración de DFS

Los espacios de nombres DFS pueden administrarse mediante:

Consola de Administración de DFS

Cmdlets de PowerShell (DFSN)

Herramienta DfsUtil

Scripts basados en WMI


# Replicación del Sistema de Archivos Distribuido (DFS)

La replicación DFS es un servicio de rol de Windows Server que permite sincronizar carpetas entre varios servidores, incluso en diferentes sitios, de forma eficiente y confiable. Está disponible en Windows Server

## ¿Qué es la replicación DFS?

Es un motor de replicación activo-activo, lo que significa que:

Los cambios pueden realizarse en cualquiera de los servidores.

Los datos se sincronizan automáticamente entre todos los miembros.

## Relación con Active Directory

AD DS usa replicación DFS para sincronizar la carpeta SYSVOL.