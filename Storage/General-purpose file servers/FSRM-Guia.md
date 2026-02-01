# Guía teórico–práctica: Administración con File Server Resource Manager (FSRM)

## 1. Establecer opciones del Administrador de recursos del servidor de archivos

### Teoría
Las opciones generales de FSRM permiten definir el comportamiento global del sistema, especialmente:
- Notificaciones por correo electrónico
- Registro de eventos
- Auditoría
- Configuración predeterminada para cuotas y filtros

Estas opciones afectan a todas las funciones de FSRM.

### Práctica
1. Abrir **Administrador del servidor**
2. Ir a **Herramientas > File Server Resource Manager**
3. Clic derecho en **File Server Resource Manager** > **Configurar opciones**
4. Configurar:
   - Servidor SMTP
   - Dirección de correo del administrador
   - Registro de eventos y auditoría

Esto es necesario antes de usar cuotas, filtros e informes.



## 2. Administración de cuotas

### Teoría
Las cuotas limitan el espacio en disco que puede usar un usuario o carpeta.
Tipos de cuotas:
- Cuota rígida: bloquea al alcanzar el límite.
- Cuota flexible: solo notifica, no bloquea.

Se basan en **plantillas de cuota** para facilitar la administración.

### Práctica
1. En FSRM, ir a **Administración de cuotas**
2. Revisar **Plantillas de cuota**
3. Crear una plantilla nueva o usar una existente
4. Crear una cuota:
   - Manual: para una carpeta específica
   - Automática: para que las subcarpetas hereden la cuota
5. Configurar:
   - Límite de espacio
   - Umbrales
   - Notificaciones

Uso típico: carpetas de usuarios.

---

## 3. Administración de filtrado de archivos

### Teoría
El filtrado de archivos permite:
- Bloquear tipos de archivos no permitidos (exe, mp3, mp4, etc.)
- Supervisar intentos de uso indebido

Puede ser:
- Activo: bloquea archivos
- Pasivo: solo registra eventos

Se basa en **grupos de archivos** y **plantillas de filtro**.

### Práctica
1. Ir a **Administración de control de archivos**
2. Revisar o crear **Grupos de archivos**
3. Revisar o crear **Plantillas de control de archivos**
4. Crear un filtro en una carpeta o volumen
5. Configurar notificaciones y eventos
6. Definir excepciones si es necesario

Uso típico: evitar uso de almacenamiento para archivos personales.

---

## 4. Administración de informes de almacenamiento

### Teoría
Los informes permiten analizar el uso del disco, por ejemplo:
- Archivos grandes
- Archivos por propietario
- Uso de cuotas
- Actividad de filtrado

Pueden ejecutarse:
- Bajo demanda
- De forma programada

### Práctica
1. Ir a **Administración de informes de almacenamiento**
2. Ejecutar un informe bajo demanda
3. Seleccionar:
   - Tipo de informe
   - Volumen o carpeta
4. Programar informes periódicos
5. Configurar envío por correo

Uso típico: auditoría y planificación de almacenamiento.

---

## 5. Administración de clasificaciones

### Teoría
La clasificación asigna propiedades a archivos según reglas, por ejemplo:
- Tipo de contenido
- Confidencialidad
- Propietario
- Ubicación

Se usa junto con **File Classification Infrastructure (FCI)**.

### Práctica
1. Ir a **Administración de clasificaciones**
2. Crear propiedades de clasificación
3. Crear reglas de clasificación:
   - Por ubicación
   - Por contenido
   - Por tipo de archivo
4. Ejecutar la clasificación manual o programada

Uso típico: cumplimiento normativo y automatización.

---

## 6. Tareas de administración de archivos

### Teoría
Las tareas permiten automatizar acciones sobre archivos clasificados, como:
- Mover archivos
- Copiarlos
- Eliminarlos
- Ejecutar scripts o comandos

Funcionan en conjunto con la clasificación.

### Práctica
1. Ir a **Tareas de administración de archivos**
2. Crear una nueva tarea
3. Definir:
   - Condición (clasificación, antigüedad, tamaño)
   - Acción (mover, eliminar, ejecutar script)
4. Programar la ejecución

Uso típico: limpieza automática y gestión del ciclo de vida de archivos.

---

## Resumen rápido

- Opciones de FSRM: configuración base obligatoria
- Cuotas: control del espacio en disco
- Filtrado: control de tipos de archivos
- Informes: análisis y auditoría
- Clasificación: etiquetado inteligente de archivos
- Tareas: automatización basada en reglas

FSRM permite administrar el almacenamiento de forma centralizada, segura y automatizada.
