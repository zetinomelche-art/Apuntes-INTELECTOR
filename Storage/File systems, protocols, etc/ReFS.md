# ReFS (Resilent File System) 

Un sistema desarrollado por microsoft que permite maximisar la disponiblilidad de los datos y proporcionar integridad de los datos con resistencia a danios.

# Resiliency
ReFS tiene caracteristica que puede detectar danios en los archivos y repararlos mientra esten en linea.

Integración de Espacios de almacenamiento: Cuando se usan volumenes espejo, y se dania uno, puede ocupar los datos del espejo para repara el danio

Corrección proactiva de errores, ademas de validar datos antes de escritua y lectura tiene un depurador que escanea cada tanto en busca de errores para corregirlos

# Rendimiento

# EScalabilidad
Diseniado para grupos de datos inmentos y que el rendimiento no se vea afectado


# Flujos de integridad de ReFS
Es una caraceteristica opcional que valida y mantiene la integridad de los datos.

# ReFSUtil
Una utilidad de linea de comandos para la reparacion de volumees, administracion y demas cosas