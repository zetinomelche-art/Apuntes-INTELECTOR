# Storage Spaces

En esencia los stogare spaces podrian parecerse a un arreglo RAID hecho por software,  integrado en windows server

Windows toma varios discos fisicos, los junta en un grupo logico y de ahi crea discos virtuales, que en windows aparecen como fisicos

# Ejemplo

Paso 1
- 5 discor fisicos (SDD, HDD, NVMe)
- Se agregan a un storage pool

Paso 2
- De ese storage pool se sacan discos virtuales
- Se ven en el administrador de discos
- Se formatena en NTFS ReFS
- Se le asigna letra

# Caracteristicas
Se pueden sacar varios discos de un solo pool
Diferente nivel de proteccion para cada disco
Expansion sin apagar el servidor

# Tipos de resistencia

##  Espacios simples

- Sin redundancia de datos
- Datos repartios entre discos
- Se usa el 100% del espacio

*Desventajas*
- Si se muere un disco se puerde todo

*Util para*
- Cache
- Archivos temporales
- Datos nada criticos

## Espacios reflejados
- Copia de los datos en 2 o 3 discos
- Existen 2 tipos 

    **Reflejo bidireccional**
    - Tolera hasta un disco caido
    - Pierde el 50% de espacio

    **Reflejo triple**
    - Soporta hasta 2 discos caidos
    - Pierde el 66% del espacio

*Util para*
- Maquinas virtuales
- Bases de datos


## Espacios de paridad
- Datos + informacion matematica (Paridad)
- Permite recontruir datos si un disco falla

    **Tipos**
    - Paridad simple, tolera 1 disco caido
    - Paridad dual, tolera hasta 2 discos caidos

- Mejor uso del espacio que espejo
-Buen rendimiento de lectura

*Util para*
- Backups
- Archivado
- Datos que se leen más de lo que se escriben

# Chache del bus de almacenamiento
Se usa un SSD o NVMe como cache
Mejora el rendimientos de discos mas lentoss como HDD

Los datos mas usados se guardan primero en la cache y luego se van al los discos lentos.




