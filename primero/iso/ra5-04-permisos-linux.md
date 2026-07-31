# Permisos GNU/Linux
En el sistema operativo GNU/Linux todo es un archivo los cuales pertenecen a un dueño y un grupo, estos permisos se dividen en tres categorias de usuarios:

1. **u(User/Owner):** El usuario que creó el archivo o quien le asigno la propiedad.
2. **g(Group):** El grupo de usuarios que tiene acceso al archivo.
3. **o(Others):** Cualquier otro usuario del sistema que no sea dueño ni pertenezca al grupo.

## Tipos de permisos básicos
Para cada una de las categorias existen tres opciones (rwx):

- **r (Read - Lectura):** Permite ver el contenido de un archivo o listar si es un directorio.
- **w (Write - Escritura):** Permite modificar el contenido del archivo o modificar el directorio.
- **x (Execute - Ejecución):** Permite ejecutar un archivo o entrar dentro si es un direcotrio o ver los metadatos de dicho directorio.

## Lectura de los permisos con `ls`

```text
- r w x r - x r - -  1 root root  148 Jul 31 20:22 script.sh
┬ ───┬── ───┬── ───┬──
│    │      │      └─ Permisos de Otros (Others) -> Lectura (4)
│    │      └─ Permisos del Grupo (Group) -> Lectura y Ejecución (4+1 = 5)
│    └─ Permisos del Propietario (User) -> Lectura, Escritura y Ejecución (4+2+1 = 7)
└─ Tipo de archivo (- = archivo común, d = directorio, l = enlace simbólico)
```