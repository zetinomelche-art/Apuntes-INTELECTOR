# LDAP (Lightweight Directory Access Protocol)

## 1. ¿Qué es LDAP?

LDAP (Lightweight Directory Access Protocol) es un **protocolo de red** que se utiliza para **acceder, consultar y administrar servicios de directorio**. Un servicio de directorio es una base de datos especializada que almacena información estructurada sobre usuarios, equipos, grupos, servicios y otros recursos dentro de una red.

LDAP no es una base de datos en sí, sino el **protocolo** que define cómo los clientes se comunican con el directorio.

Un ejemplo muy común de servicio de directorio que utiliza LDAP es **Active Directory** en Windows Server.

---

## 2. ¿Para qué se utiliza LDAP?

LDAP se usa principalmente para:

* Autenticación de usuarios (inicio de sesión)
* Autorización (permisos y accesos)
* Búsqueda de información en un directorio
* Administración centralizada de identidades

En entornos empresariales, LDAP permite que los usuarios usen **una sola cuenta** para acceder a múltiples servicios.

---

## 3. ¿Qué tipo de información almacena LDAP?

Un directorio LDAP puede almacenar:

* Usuarios
* Contraseñas (de forma cifrada)
* Grupos
* Equipos
* Impresoras
* Políticas y atributos personalizados

Cada objeto tiene **atributos**, por ejemplo:

* Un usuario puede tener: nombre, apellido, correo, nombre de inicio de sesión, etc.
* Un equipo puede tener: nombre del host, sistema operativo, ubicación.

---

## 4. Estructura del directorio LDAP

LDAP utiliza una estructura **jerárquica**, similar a un árbol.

Ejemplo de estructura:

```
DC=empresa,DC=com
 ├── OU=Usuarios
 │    └── CN=Juan Perez
 ├── OU=Equipos
 │    └── CN=PC-01
```

Donde:

* **DC (Domain Component)** representa el dominio
* **OU (Organizational Unit)** organiza objetos
* **CN (Common Name)** identifica al objeto

Esta estructura facilita la administración y búsqueda de información.

---

## 5. ¿Cómo funciona LDAP?

El funcionamiento básico es el siguiente:

1. Un cliente (PC, aplicación o servicio) envía una solicitud LDAP.
2. El servidor LDAP procesa la solicitud.
3. El servidor responde con la información solicitada o con el resultado de la autenticación.

Ejemplos de operaciones LDAP:

* **Bind**: autenticarse en el directorio
* **Search**: buscar objetos
* **Add**: agregar objetos
* **Modify**: modificar atributos
* **Delete**: eliminar objetos

---

## 6. Puertos utilizados por LDAP

LDAP utiliza los siguientes puertos:

* **389/TCP**: LDAP sin cifrado
* **636/TCP**: LDAPS (LDAP sobre SSL/TLS)

En entornos productivos se recomienda usar **LDAPS** para proteger la información.

---

## 7. LDAP y Active Directory

Active Directory usa LDAP como uno de sus protocolos principales para:

* Consultar usuarios y grupos
* Autenticar cuentas
* Aplicar políticas y permisos

Cuando un usuario inicia sesión en un dominio Windows, el sistema utiliza LDAP para consultar la información del usuario dentro del directorio.

---

## 8. Ventajas de LDAP

* Administración centralizada
* Escalable para grandes organizaciones
* Compatible con múltiples sistemas operativos
* Permite integración con aplicaciones y servicios externos

---

## 9. Ejemplo práctico

Cuando un usuario intenta iniciar sesión en un sistema:

1. El sistema consulta al servidor LDAP.
2. LDAP verifica si el usuario existe.
3. Comprueba la contraseña.
4. Devuelve si el acceso es permitido o denegado.

---

## 10. Conclusión

LDAP es un protocolo fundamental en redes empresariales. Permite gestionar identidades, autenticar usuarios y organizar recursos de forma centralizada y segura. En entornos Windows Server, LDAP es una pieza clave del funcionamiento de Active Directory.
