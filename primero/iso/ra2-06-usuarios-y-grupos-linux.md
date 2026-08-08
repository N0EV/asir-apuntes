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
| :---- | :---- |
| /etc/passwd | información básica de los usuarios |
| /etc/shadow | contraseñas cifradas y envejecimiento |
| /etc/group | infomación de grupos |
| /etc/skel | archivos iniciales de home de cada usuario |
| /etc/adduser.conf | configuración del comando adduser |
| /etc/deluser.conf | configuración del comando deluser |

## Fichero /etc/passwd
Guarda la información básica de los usuarios. Cada línea tiene el formato:

`usuario:x:uid:gid:gecos:home:shell`

Esto se desglosaría de la siguiente forma:

- **usuario:** Nombre del usuario para el sistema.
- **x**: Su password es decir si tiene contraseña normalmente guardada en /etc/shadow.
- **uid:** el id del usuario.
- **gid:** el id del grupo.
- **gecos:** nombre real e información adicional.
- **home:** directorio personal del usuario.
- **shell:** intérprete al iniciar sesión es decir su shell.

## Fichero /etc/shadow
Guarda las contraseñas de forma cifrada y la información de envejecimiento de las mismas, unicamente root puede ver su contenido.

El formato en el que se guarda es el siguiente:

`usuario:password:lastchg:min:max:warn:inactive:expire:unused`
Esto se deslgosaría de la siguiente forma:

- **usuario:** el usuario al que se hace referencia en esa línea.
- **password:** la contraseña del usuario cifrada. Si aparece un `!` es que la cuenta esta bloqueada.
- **lastchg:** días desde 1/1/1970 del último cambio.
- **min:** días mínimos antes de poder volver a cambiar contraseña.
- **max:** días hasta que caduca.
- **warn:** días antes del vencimiento para avisar.
- **inactive:** 0 si caduca la cuenta se bloquea y -1 puede seguir entrando para cambiarla.
- **expire:** fecha en el que la cuenta deja de funcionar.

## Gestión de usuarios
### Creación de usuarios
Para la creación de usuarios se usa el comando `useradd` este es de bajo nivel.

Algunas de las opciones son:
- **`-g`:** grupo principal
- **`-d`:** directorio home
- **`-m`:** crea el home
- **`-s`:** shell

Un ejemplo de este comando seria el siguiente:

```bash
sudo useradd -g grupo1 -d /home/usuario -m -s /bin/zsh usuario
```
Otro comando que se puede usar es `adduser`este es de alto nivel y puedes hacer todo de forma interactiva.

Su funcionamiento principal es el siguiente:
- Copia `/etc/skell`.
- Pide datos.
- Configurado por `/etc/adduser.conf`.


El uso más típico en el que se suele usar es que para usuarios normales se use `adduser` y para usuarios del sistema o creación másiva se user `useradd`

### /etc/skell
Esta ruta se usa para copiar y montar el home de cada usuario nuevo que se cree en el sistema.

### Modificar o eliminar usuarios
Algunos de los comandos para hacer esto son:

- **usermod:** modificar una cuenta, por ejemplo para añadir un grupo secudnario. Ejemplo:

```bash
sudo usermod -aG grupo usuario
```

- **userdel:** eliminar usuario, este también es de bajo nivel.

- **deluser:** eliminar usuario, este es de alto nivel con opciones extra y esta controla do por `/etc/deluser.conf`.

## Gestión de contraseñas
Los comandos principales para esto son:
- **paswd:** para cambiar la contraseña. Ejemplo: `paswwd usuario`.
- **change:** para configurar el envejecimiento. Ejemplo: `chage usuario`.

## Grupos
Los grupos nos permiten manejar a grupos grandes de usuarios de forma mas comoda. El fichero principal donde se guarda esto es `/etc/group`.

Y dentro de este el formato es el siguiente:

`grupo:x:gid:lista-usuarios`

Esto se desglosa de la siguiente forma:

- **grupo:** nombre del grupo.
- **x:** si este tiene contraseña.
- **gid:** id el grupo.
- **lista-usuarios:** usuarios secundarios separados por comas.

Dentro de los grupos hay de varios tipos los secundarios y los primarios.

Los primarios estan guardados en `/etc/passwd`.
Los secundarios estan guardados en `/etc/group`.

El comportamiento varia segun que tipo de grupos tiene cumpliendose lo siguiente:

- Al crear archivos, el grupo con el que se asocian dichos archivos es el primario del usuario.
- Para los permisos del grupo, cuentan todos los grupos a los que un usuario pertenece.

## Comandos para la gestión de grupos
Algunos de los comandos más usuados son los siguientes.

| Comando | Función |
| :---- | :---- |
| groupadd | Crear grupo |
| groupmod | Modificar grupo |
| groupdel | Eliminar grupo |
| groups | Ver grupos |
| id | Ver uid, gid y grupos |
| newgrp | Cambiar temporalmente el grupo primario |

Ejemplos de dichos comandos:

```bash
# Crear grupos
sudo groupadd grupo

# Añadir usuario a grupo secundario (POSIX):
sudo usermod -aG grupo1 usuario

# Cambiar grupo primario
sudo usermod -g grupo1 grupo2

# Ver los grupos a los que pertences
sudo groups
```

## Usuarios y grupos estándar del sistema
Los grupos estandar del sistema se dividen en dos por su uid.

1. Usuarios del sistema el uid es menor que 100, mientras que los usuarios normales es mayor o igual a 1000.

### El usuario root
Este usuario es el "rey" del SO y tiene el UID 0. Normalmente está desactivado por seguridad. Para tareas administrativas se suele usar el comando `sudo` (*superuser do*), pero el usuario que lo ejecute debe pertenecer al grupo `sudo`.

Para poder habilitar root con el siguiente comando sería suficiente.

```bash
sudo passwd root
```

Para deshabilitarlo este otro comando:

```bash
sudo passwd -1 root
```

Para añadir usuarios al grupo sudo se puede hacer de dos formas.

```bash
# Con adduser
sudo adduser usuario sudo

# Con usermod
sudo usermod -a -G sudo usuario
```

Para eliminar a dichos usuarios del grupo sudo, de la siguiente forma.

```bash
sudo deluser usuario sudo
```

Para los grupos secundarios de los usuarios usamos `usermod`, simplente dejas los grupos a los que si quieres que pertenezca el usuario y esto sobreescribira los grupos a los que ya pertenece. Por ejemplo el usuario llamado usuario pertence a los grupos grupo1, grupo2 y grupo3 y quieres quitar grupo3, para esto harías lo siguiente:

```bash
sudo usermod -G grupo1,grupo2 usuario
```

## Comando `su`
Este comando nos permite cambiar de usuario, pide la contraseña del usuario al que nos queremos cambiar.

Ejemplos:

```bash
su #Esto cambia a root
su usuario #Esto cambia al usuario especificado
```

## Devian vs POSIX
Las principales diferencias son:
- Debian: scripts, Perl, interactivos, seguros, basados en /etc/adduser.conf
- POSIX: binarios, C, silenciosos, portables, orientados a scripts

Ejemplos:
```bash
sudo adduser usuario #Interactivo
sudo useradd -m -s /bin/bash usuario #No interactivo
sudo passwd juan
```
Cuando se debe usar cada uno:
- Para uso de manual Debian/Ubuntu se debe usar comandos Debian.
- Para uso de scripts portables se debe usar comandos POSIX.

## Algunos comandos más

Algunos de los coamndos que faltan son los siguientes:

```bash
# Para ver los logins exitosos
last

# Para ver los intentos de login fallidos
lastb

# Para ver los usuarios conectados en ese momento
who

# Para ver usuarios + los procesos
w
```