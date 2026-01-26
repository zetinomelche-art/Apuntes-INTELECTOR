# Active Directory Certificate Service
Es un rol de WS que permite la creacion y administracion de certificados de infraestructura de clave publica,
mediante metodos de autenticacion y comunicacion seguros.



Se usa para cifrar y firmar documentos digitales, cuentad de usuarios y equipos.

-Confidencialidad mediate el cifrado
-Integridad mediante la firma

Una infraestructura de clave pública PKI (Public Key Infraestructure) consta de un conjunto de hardware, software y procedimientos para la emisión, almacenamiento, consulta y revocación de certicados digitales

# IMPORTANTE
La tecnología PKI permite a las entidades autenticarse frente a otras entidades y usar la información de los certificados, generalmente las claves públicas, para cifrar y descifrar mensajes.
Los usos de la tecnología PKI se relacionan con:
    La autenticación de usuarios y sistemas
    La identificación del interlocutor
    EI cifrado de datos digitales
    La firma digital de datos, documentos, software, etc.
    La seguridad de las comunicaciones
    La garantía de no repudio

# CA (CArtifiacate Autority)
Es la encarga de emitir y revocar certificados. Es la entidad que da legitimidad a la relacion de una calve publica y un usuario o servicio

# RA (Registration Autority)
la encargada de verificar el enlace entre certificados, entre la calve publica del certificado y la identidad de sus titulares

# Repos
donde se almacenan a informacion de las PKI.
Los repositorios de certificados
Las repos de CRL (Certificate Revoque List)

# VA (Validation Autority)
Es la encargada de verificar la validez de un certificado


# Permite cubrir las siguintes necesidades 
    Redes inalámbricas seguras
    Redes privadas virtuales
    Cifrado de archivos
    Uso del protocolo SSL


## caracteristicas clave

-Entidades de certifiacion:La entidad raiz y subordinadas, se utlisan para la creacion y validacion de certificados, para usuarios, equipos o servicios.

-Inscripción web de entidad de certificación en servicios de certificados de AD: Permite a los usurios conectarse mediante el navegador a una entidad certificadora para hacer solitar un certificado y recuperar CRL (Certificate Revoque Lists)

-servicio web de inscripción de certificados:El servicio web de inscripción de certificados es un servicio de rol de Servicios de certificados de Active Directory (AD CS) que permite a los usuarios y equipos realizar la inscripción de certificados mediante el protocolo HTTPS. Junto con el servicio web directiva de inscripción de certificados, esto habilita la inscripción de certificados basada en directivas cuando el equipo cliente no es miembro de un dominio o cuando un miembro de dominio no está conectado al dominio.

-Respondedor en linea: Decodifica una solicitud de estado de revocacion(Verifica si es valido  o no) y devuelve una respuesta firmada con la info solicitada sobre el estado de un certificado.

-Servicio de inscripcion de dispositivos de red: Per ite a dispositivos como routers y otros dispositivos de red obtener un certificado que son los que no disponen de cuentas de dominio

-Verifiacion de claves TMP: Verifica que a la Autoridad Certificadora verificar que:
                            - la clave privada del certificado se gennero y se guarda dento de un TMP fisico
                            - Que el TPM sea legitimo, es decir que no sea un software emulado

- Servicio web de directiva de inscripción de certificados: Permite al usuarios y equipos consultar sobre directivas de inscripcion de certificados


## Plantillas de certificados
Permite emitir y administrar certificados ya preconfigurados para facilitar la gestion de los certificados
