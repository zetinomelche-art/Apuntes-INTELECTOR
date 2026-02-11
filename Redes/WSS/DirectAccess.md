# DirectAccess

Es lo que permite que los equipos remostos esten automaticamente conectados a la red de la empresa sin necesidad de una VPN.

- La conexión es automática, permanente y transparente para el usuario.

# Como funciona

El usuario está fuera de la empresa (casa, hotel, café)

El equipo:
    - Se conecta a Internet
    - Detecta que no está en la red corporativa

Automáticamente:

    - Establece un túnel seguro con el servidor DirectAccess

El equipo:

    - Accede a recursos internos (AD, archivos, apps)
    - Puede ser administrado por TI (GPO, parches, scripts)

El tunel se establece antes incluso de que el usuario inicie sesion

# Requisitos importantes
Windows 11 Enterprise
Windows 10 Enterprise
Windows 10 Enterprise LTSB
Windows 8.1 Enterprise

Windows Server (2016+)


# Beneficios principales

## Para usuarios

No hacer nada
Experiencia “como en la oficina”
Menos problemas de conexión

## Para TI

Administración remota continua
Aplicar GPOs
Instalar parches
Ejecutar scripts
Diagnóstico remoto


# Microsoft recomienda usar Always On VPN en lugar de DirectAccess para nuevas implementaciones.

¿Por qué?

DirectAccess:

Es complejo
Difícil de mantener
Depende de tecnologías antiguas (IPv6 transición)

Always On VPN:

Más flexible
Mejor integración moderna
Funciona mejor con cloud/híbrido

# DirectAccess no esta muerto, pero ya no es el futuro.