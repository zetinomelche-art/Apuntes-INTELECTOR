# Estorage Replica

# Que es?
Es una tecnoligia de windows server que permite copiar datos en tiempo real, de un servidor(o cluster), a otro, para recuperacion de desastres

# Sirve para
- Fallas de hardware
- Medidas preventivas ante desastres
- Mantenimiento planificado

# Terminos

- RPO (Recovery Point Objective) *Objetivo de punto de recuperacion*
Define la cantidad maxima de perdida de datos

- RTO (Recovery Time Objective) *Obtivo de tiempo de recuperacion*
Tiempo maximo para restaurar una app o servicio

- Failover 
Mecanismo que transfiere operaciones de un servidor a otro, cuando el principal falla


# Tipos de replicacion

- Sincrona
Necesita de una red rapida y con baja latencia

-- *Ideal para* 
Bases de datos
Datos criticos
Sitios que esten relativamente cerca


- Asincrona
Mejor rendimiento 
Mejor para largs distancias
Si ocurre una falla podria hacer pequenias perdidas de datos
Ideal donde RPO(Recovery Point Object) > 0

# En que nivel trabaja el Storage Replica

A nivel de bloque y particion, no de archivos.
Esto significa que replica todo, absolutamente todo.

*Si se borra algo en un lado, se borra en el otro, no reemplaza a un Backup*


# caracteristicas
Usa SMB 3
Cofrado AES 128/ Kerberos
Compresion 

# Windows Server Standar vs Datacenter

- Windows Server Standar 
Solo 1 volumen
2tb Maximo
Desde la version 2019

- Datacenter
Todo ilimitado

# Configuraciones posibles

## Clúster extendido (Stretch Cluster)
UN SOLO clúster de Windows Server,
pero sus nodos están en DOS (o más) sitios físicos distintos,
y los datos se replican entre esos sitios usando Storage Replica.

Sigue siendo un solo clúster, aunque esté “partido” geográficamente.

Failover automatico


## Clúster a clúster
- 2 closteres distitos
- Replicacion entre ellos
- failover manual

Ejemplo: Cluster en Santa Ana <-> Custer en San Salvador

## Server a server
- 2 servers independientes
- Sin cluster
- Failover manual


# Registro de storage server
1 Anota cada escritura de en un registro (log)
2 Luego se replica en el destino
3 Los datos se escriben en el disco en el volumen destino

*Si se crea una replica con regsitro tradicional, no se puede cmabiar a registro mejorado*

## Cuando se usa
- Cargas intensivas (SQL, VMs, archivod grandes)
- Redes rapidas
- Mejor rendimiento
- Menos latencia
- El registro tradicional es menos escalable
