# Usuarios y grupos
GNU/Linux es un sistema multiusuario, lo que significa que varios usuarios pueden estar trabajando al mismo tiempo, localmente o de forma remota.

Para usar el sistema, cada usuario necesita dos cosas: Nombre de usuario y Contraseña

Las cuentas se gestioan desde root, el administrador con uid 0 y permisos totales.

Los usuarios pueden ejecutar aplicaciones según sus permisos. Estos se usan con grupos para asignar permisos comunes a varios usuarios sin configurar previamente.

### Identificadores

uid --> identificador del usuario
gid --> identificador del grupo primario del usuario
Root tiene uid y gid 0

### Relación usuarios - procesos - archivos
Todo proceso pertenece a un usuario y a un grupo primario y todo archivo tiene un propietario y un grupo, esto se puede ver con el comando `ls -l`.

## Ficheros de configuración
Todos los /etc.

Estos son:

| Archivo | Función |
| /etc/passwd | información básica de los usuarios |
| /etc/shadow | contraseñas cifradas y envejecimiento |
| /etc/group | infomación de grupos |
| /etc/skel | archivos iniciales de home de cada usuario |
| /etc/adduser.conf | configuración del comando adduser |
| /etc/deluser.conf | configuración del comando deluser |

## Fichero /etc/passwd
Guarda la información básica de los usuarios. Cada línea tiene el formato:

`usuario:x:uid:gid:gecos:home:shell`

