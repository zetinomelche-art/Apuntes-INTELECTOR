# Verificar que los servicios principales estén corriendo

PS:
Get-Service NTDS,DNS,Netlogon,KDC

Deberían aparecer en estado:

Status : Running


Servicios importantes:

    NTDS → Active Directory Domain Services
    DNS → Servidor DNS
    Netlogon → Autenticación y registro de equipos
    KDC → Kerberos

# Verificar estado general del DC (diagnóstico completo)

PS:
dcdiag

CMD:
dcdiag /v

# Verificar que este corriendo registrado en DNS
dcdiag /test:dns

# Reiniciar el DC
PS:
Restart-Service NTDS
Restart-Service DNS
Restart-Service Netlogon