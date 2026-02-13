# Reiniciar DNS

PS
Restart-Service DNS 

CMD
net stop dns
net start dns

# Ver el estado
Get-Service DNS


#  Restablecer la chache

PS
Clear-DnsServerCache -Force

CMD
ipconfig /flushdns
Clear-DnsServerCache