Cuando hay mas de un domimio se le llama, arbol de dominio.

un dominio permite, controlar los recursos del dominio

# Colocar un IP estatica en el Server


# Promover como DC 

Installation Type
    > Role-based or feature-based installation
        > Server Selection
            > Select a server from the server pool
                > Server Roles
                    > Active Directory Domain Services
                        > Add required features
                            > Features
                                > Default (no cambios)
                                    > AD DS
                                        > Next
                                            > Confirmation
                                                > Install

# AD en modo replica
Los mismos pasos que el anterior solo que sin promover como controlador de dominio

Deployment Configuration
    > Select deployment operation
    Add a domain controller to an existing domain
        > Domain
        dominio.local
        Credentials
        Domain 
        Admin


```bash
repadmin /showrepl

repadmin /replsummary

readmin /syncall

repadmin /syncall /AdeP
```