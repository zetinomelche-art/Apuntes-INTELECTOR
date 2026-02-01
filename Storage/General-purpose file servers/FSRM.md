# File System Resource Manager

Permite administrar y clasificar los datos almacenados en servidores de archivos.
Puede clasificar automaticamente archivos, tareas basadas en la clasificacion y la administracion de cuotas en carpetas.

# Caracteristicas Primera parte

## Administracion de Cuotas
- Limite de esoacion perimitido para una carpeta o un volumen.
- Es posible la creacion de plantillas de cuotas.

## Infraestructura de clasificacion
Es pisible automatixar tareas para la clasificacion de archivos, para poder aadministrar los datos de manera mas eficaz. Es posible clasificar estos datos paara aplicar politacs de grupo.

## Tareas de Administracin de archivos 
Aplicar una directiva condifcional a archivos segun su clasificacion

## Administración de filtrado de archivos
Controlar los tipos de archivos que los usuarios ppueden alamcenar en el servidor de archivos
Es posible limitar las extensiones de archivos que almacenan en el server. Ejemplo: Un filtro que no permita archivos .mp3 en carptas compartidas o personales en un servidor de archivos.

## Informaes de almacenamiento
Para ayudar a visualizar tendencias de uso del disco y como se claifican los datos. 
Supervisar un grupo de usuarios en concreto para asuditar intentos de guardar archivos no autorizados.

## Notificaciones 
Configure los parámetros de correo electrónico si tiene pensado enviar por correo electrónico notificaciones de umbral o informes de almacenamiento. 


# Lista de comprobación: Aplicar una cuota a un volumen o carpeta
Aplica a: Windows Server 2016, 2019, 2022 y 2025

## 1. Configurar notificaciones por correo
Antes de crear cuotas, configure los parámetros de correo electrónico si desea:
- Recibir alertas cuando se alcance un umbral de espacio.
- Enviar informes automáticos de almacenamiento.

Esto se realiza desde la configuración de notificaciones por correo de File Server Resource Manager (FSRM).

## 2. Analizar el uso de almacenamiento
Evalúe cómo se está usando el espacio en el volumen o carpeta:
- Utilice los informes de almacenamiento de FSRM.
- Ejecute informes bajo demanda, como “Archivos por propietario”, para identificar usuarios que consumen más espacio.

Este paso ayuda a definir límites de cuota adecuados.

## 3. Revisar o crear plantillas de cuota
Puede elegir una de las siguientes opciones:
- Usar una plantilla de cuota preconfigurada.
- Crear una nueva plantilla personalizada según las políticas de la organización.

Las plantillas permiten reutilizar configuraciones de cuotas de forma consistente.

## 4. Aplicar la cuota
Aplique la cuota usando una plantilla:
- Crear una cuota manual en un volumen o carpeta específica.
- O crear una cuota automática para que las subcarpetas hereden la cuota automáticamente.

Las cuotas automáticas son ideales para carpetas de usuarios.

## 5. Supervisar el uso de las cuotas
Programe tareas de informes periódicos:
- Incluya informes de uso de cuotas.
- Revise regularmente estos informes para controlar el consumo de espacio y prevenir problemas.

Esto permite una administración proactiva del almacenamiento.




# Lista de comprobación: Aplicar una cuota a un volumen o carpeta


## 1. Configurar notificaciones por correo electrónico
Configure los parámetros de correo electrónico si desea:
- Recibir notificaciones cuando se alcance un límite de cuota.
- Enviar informes automáticos de almacenamiento.

Esto se realiza desde la configuración de notificaciones por correo de File Server Resource Manager (FSRM).

## 2. Evaluar los requisitos de almacenamiento
Antes de aplicar una cuota:
- Analice el uso actual del volumen o carpeta.
- Utilice los informes del módulo Administración de informes de almacenamiento.
- Ejecute informes bajo demanda, como “Archivos por propietario”, para identificar a los usuarios que consumen más espacio en disco.

Este análisis ayuda a definir límites de cuota adecuados.

## 3. Revisar o crear plantillas de cuota
Seleccione una de las siguientes opciones:
- Revisar y usar una plantilla de cuota preconfigurada.
- Crear una nueva plantilla de cuota para aplicar una política de almacenamiento personalizada en la organización.

Las plantillas permiten aplicar cuotas de forma estandarizada.

## 4. Crear la cuota
Aplique la cuota utilizando una plantilla:
- Crear una cuota manual en un volumen o carpeta específica.
- O crear una cuota automática para que todas las subcarpetas hereden la cuota automáticamente.

Las cuotas automáticas son recomendadas para carpetas de usuarios.

## 5. Supervisar el uso de las cuotas
Programe tareas de informes periódicos:
- Incluya informes de uso de cuotas.
- Revise estos informes regularmente para controlar el consumo de espacio y prevenir problemas de almacenamiento.

Esto permite una administración continua y proactiva del espacio en disco.


# Lista de comprobación: Aplicación de un filtro de archivos a un volumen o carpeta

## 1. Configurar notificaciones por correo electrónico
Configure las opciones de correo electrónico si desea:
- Enviar notificaciones cuando se bloquee o detecte un archivo.
- Recibir informes automáticos relacionados con el filtrado de archivos.

Esto se configura desde File Server Resource Manager (FSRM).

## 2. Habilitar auditoría de filtrado de archivos
Si necesita generar informes de auditoría:
- Active el registro de eventos de filtrado de archivos.
- Los eventos se almacenarán en la base de datos de auditoría.

Esto permite llevar control sobre intentos de guardar archivos bloqueados.

## 3. Analizar los tipos de archivos almacenados
Antes de aplicar filtros:
- Evalúe qué tipos de archivos existen en el volumen o carpeta.
- Use los informes de Administración de informes de almacenamiento.
- Ejecute informes bajo demanda como:
  - Archivos por grupo de archivos
  - Archivos grandes

Este análisis ayuda a definir reglas de filtrado adecuadas.

## 4. Revisar o crear grupos de archivos
Seleccione una opción:
- Usar grupos de archivos preconfigurados (por ejemplo, archivos de audio, video o ejecutables).
- Crear nuevos grupos de archivos personalizados según la política de la organización.

Los grupos de archivos definen qué extensiones serán controladas.

## 5. Revisar o crear plantillas de filtro de archivos
Puede:
- Revisar y usar plantillas de filtro de archivos existentes.
- Crear una nueva plantilla de filtro para aplicar una política específica.

Las plantillas permiten reutilizar reglas de filtrado fácilmente.

## 6. Crear el filtro de archivos
Aplique el filtro usando una plantilla:
- Cree un filtro de archivos en un volumen o carpeta específica.

Esto activa el bloqueo o supervisión de los tipos de archivos definidos.

## 7. Configurar excepciones
Si es necesario:
- Defina excepciones de filtrado en subcarpetas.
- Las excepciones permiten permitir ciertos archivos donde el filtro general no aplica.

## 8. Supervisar la actividad de filtrado
Programe tareas de informes periódicos:
- Incluya informes de auditoría de filtrado de archiv





#


