Verificar servicios de AD
```bash
Get-Service -Name ADWS,KDC,NETLOGON,DNS
```

# Test de DNS
```bash
dcdiag /test:dns
```

# Ver puertos abiertos
```bash
Test-NetConnection -ComputerName DC-RPL -Port 389  # LDAP
Test-NetConnection -ComputerName DC-RPL -Port 88   # Kerberos
Test-NetConnection -ComputerName DC-RPL -Port 53   # DNS
```
# Limpiar caché DNS
```bash
Clear-DnsClientCache
ipconfig /flushdns
```

# Registrar en DNS
```bash
ipconfig /registerdns
```