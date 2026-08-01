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
Para ver los permisos de un directorio sin listar su contenido, se usa la opción `-d` combinada con `-l`:

```bash
$ ls -ld <nombre_directorio>
drwxr-xr-x  2 usuario  grupo  4096 ago  1 18:00 nombre_directorio/
```

Otro de los comandos para ver permisos con detalle es `stat`
```bash
$ stat <nombre_directorio>
  File: nombre_directorio
  Size: 4096            Blocks: 8          IO Block: 4096   directory
Device: 7,4     Inode: 1310780     Links: 10
Access: (0777/drwxrwxrwx)  Uid: ( 1000/ususario)   Gid: ( 1000/grupo)
Access: 2026-07-31 18:24:12.738478268 +0000
Modify: 2026-07-31 18:24:12.688478271 +0000
Change: 2026-07-31 18:24:12.688478271 +0000
 Birth: 2026-07-23 17:50:04.897900365 +0000
```
>[!NOTE]
>Para ver más información puedes hacer `man stat`, esto sacara el manual del comando stat.

## Gestión de los permisos
Para poder gestionar los permisos en GNU/Linux usamos el coamndo `chmod` (Change Mode).
Este comando tiene varias formas de usuarse.

### Forma Octal
Esta forma es la más rápida pero no permite hacer cambios de forma detallada.

La forma octal utiliza números del **0 al 7** para asignar permisos. Cada dígito representa a un tipo de usuario y está compuesto internamente por **3 bits** de información.

Cada uno de los tres dígitos de un comando `chmod` (por ejemplo, el `7`, el `5` o el `4`) se calcula sumando el valor de sus tres bits internos: **Lectura (4), Escritura (2) y Ejecución (1)**.

Visualmente, un solo dígito se divide así:

```text
       ┌─────────── Dígito Octal ───────────┐
       │                                   │
     Bit 3               Bit 2           Bit 1
  ┌─────────┐         ┌─────────┐     ┌─────────┐
  │  Read   │         │  Write  │     │ Execute │
  │   (r)   │         │   (w)   │     │   (x)   │
  └─────────┘         └─────────┘     └─────────┘
       ▲                   ▲               ▲
       │                   │               │
       4                   2               1
```

#### Tabla de Combinaciones Posibles
Al encender (`1`) o apagar (`0`) estos bits, obtenemos el valor octal final:

| Binario | Suma de Valores | Número Octal | Permiso Resultante |
| :---: | :---: | :---: | :---: |
| `0 0 0` | 0 + 0 + 0 | **0** | `---` (Ninguno) |
| `0 0 1` | 0 + 0 + 1 | **1** | `--x` (Solo ejecución) |
| `0 1 0` | 0 + 2 + 0 | **2** | `-w-` (Solo escritura) |
| `1 0 0` | 4 + 0 + 0 | **4** | `r--` (Solo lectura) |
| `1 0 1` | 4 + 0 + 1 | **5** | `r-x` (Lectura y ejecución) |
| `1 1 0` | 4 + 2 + 0 | **6** | `rw-` (Lectura y escritura) |
| `1 1 1` | 4 + 2 + 1 | **7** | `rwx` (Permisos totales) |

Cuando pasamos tres números a `chmod`, estamos aplicando este sistema de 3 bits a tres niveles de acceso diferentes: **Dueño (User), Grupo (Group) y Otros (Others)**.

```text
             chmod     7         5         5     <archivo>
                       │         │         │
       ┌───────────────┘         │         └───────────────┐
       ▼                         ▼                         ▼
 1º Dígito: DUEÑO          2º Dígito: GRUPO          3º Dígito: OTROS
 ┌───┬───┬───┐             ┌───┬───┬───┐             ┌───┬───┬───┐
 │ r │ w │ x │             │ r │ - │ x │             │ r │ - │ x │
 ├───┼───┼───┤             ├───┼───┼───┤             ├───┼───┼───┤
 │ 4 │ 2 │ 1 │             │ 4 │ 0 │ 1 │             │ 4 │ 0 │ 1 │
 └───┴───┴───┘             └───┴───┴───┘             └───┴───┴───┘
   Suma = 7                  Suma = 5                  Suma = 5
```

Ejemplo de uso en la terminal:

```bash
$ chmod 755 <nombre_archivo>
```

### Forma Simbólica

A diferencia del modo octal, el modo simbólico te permite realizar **cambios quirúrgicos**. Puedes añadir, quitar o igualar permisos específicos para un usuario concreto sin alterar el resto de la configuración del archivo.

#### La Sintaxis Básica

Cualquier comando `chmod` en modo simbólico sigue estrictamente esta estructura:

```text
       chmod   [¿A quién?]   [¿Qué acción?]   [¿Qué permiso?]   <archivo>
                   │               │                 │
              u, g, o, a        +, -, =           r, w, x
```

##### Glosario de Referencia Rápida

| **¿A quién? (Usuarios)** | **¿Qué acción? (Operadores)** | **¿Qué permiso? (Básicos)** |
| :--- | :--- | :--- |
| `u` : **u**ser (Dueño) | `+` : **Añadir** el permiso | `r` : **r**ead (Lectura) |
| `g` : **g**roup (Grupo) | `-` : **Quitar** el permiso | `w` : **w**rite (Escritura) |
| `o` : **o**thers (Otros) | `=` : **Igualar** (fija solo ese) | `x` : e**x**ecute (Ejecución) |
| `a` : **a**ll (Todos: `ugo`) | | |


#### Permisos Especiales Avanzados (`X`, `s`, `t`)

Además de las letras básicas (`r, w, x`), existen modificadores especiales que resuelven problemas específicos:

##### La `X` Mayúscula (Ejecución Condicional)
Es uno de los comandos más útiles cuando trabajas de forma recursiva (`-R`) con carpetas llenas de archivos.
* **Problema:** Si haces `chmod -R +x <carpeta>`, darás permiso de ejecución tanto a las carpetas como a las imágenes, PDFs y archivos de texto que haya dentro.
* **Solución (`+X`):** Solo añade el permiso de ejecución a los **directorios** (para que puedas entrar en ellos) y a los archivos que **ya tenían algún permiso de ejecución previamente**. No toca los archivos normales.

```bash
$ chmod -R a+X <nombre_carpeta>
# Da acceso de ejecución seguro a todo el árbol de directorios
```

##### La `s` (SUID y SGID)
Permite que un archivo o directorio se ejecute con los privilegios del dueño o del grupo, en lugar de los privilegios del usuario que lo lanza.
* **SUID (`u+s`):** Si un usuario ejecuta el archivo, este se ejecuta temporalmente con los privilegios del **dueño** del archivo (ejemplo clásico: el comando `passwd` para cambiar contraseñas).
* **SGID (`g+s`):** Si se aplica a un **directorio**, cualquier archivo nuevo creado dentro de él heredará automáticamente el **grupo** de la carpeta madre, en lugar del grupo del usuario que lo creó. Ideal para carpetas compartidas en equipo.

```bash
$ chmod g+s <carpeta_compartida>
```

##### La `t` (Sticky Bit o Bit de Permanencia)
Se aplica principalmente a directorios comunes o compartidos (como `/tmp`).
* **Función (`+t`):** Protege los archivos dentro de una carpeta. Aunque todos tengan permisos de escritura en la carpeta, **solo el dueño de un archivo puede borrarlo o renombrarlo**. Evita que los usuarios se borren cosas entre sí.

```bash
$ chmod +t <carpeta_publica>
```

- Ejemplos Prácticos para la Terminal

Puedes combinar múltiples cambios separándolos con una coma `,` (sin espacios):

```bash
# 1. Añadir ejecución al dueño y quitar escritura al grupo/otros
$ chmod u+x,go-w <archivo>

# 2. Hacer que un script sea ejecutable para todo el mundo
$ chmod a+x <script.sh>

# 3. Forzar a que el grupo tenga exactamente lectura y ejecución (borra escritura)
$ chmod g=rx <archivo>
```

## Gestión de propietarios
Para poder cambiar un recurso ya sea directorio o archivo usamos `chown`  para cambiar el usuario y `chgrp` para cambiar el grupo.

Aunque el comando `chown` a avanzado y ahora tiene la capacidad de cambiar tambien el grupo del recurso, puedes seguir usando el comando `chgrp`.

* `chown` (change owner): Para cambiar el **usuario** propietario.
* `chgrp` (change group): Para cambiar el **grupo** propietario.


### Uso Tradicional (Separado)

#### Cambiar solo el usuario (`chown`)
```bash
$ sudo chown <nuevo_usuario> <recurso>
```

#### Cambiar solo el grupo (`chgrp`)
```bash
$ sudo chgrp <nuevo_grupo> <recurso>
```

### El comando moderno: `chown` unificado
Aunque `chgrp` sigue existiendo, el comando `chown` ha evolucionado y hoy en día permite gestionar **tanto el usuario como el grupo al mismo tiempo** utilizando el separador de dos puntos (`:`). Esto hace que `chgrp` sea casi obsoleto en el uso diario.

#### Cambiar usuario y grupo a la vez
```bash
$ sudo chown <nuevo_usuario>:<nuevo_grupo> <recurso>
```

#### Cambiar solo el grupo usando `chown`
Si dejas el espacio del usuario vacío antes de los dos puntos, cambias únicamente el grupo (actúa exactamente igual que `chgrp`):

```bash
$ sudo chown :<nuevo_grupo> <recurso>
```

### Aplicación en masa (Recursivo)
Si necesitas cambiar el propietario de una carpeta y **todo lo que contiene dentro** (subcarpetas y archivos), debes añadir la opción `-R` (recursivo) en mayúscula:

```bash
$ sudo chown -R <usuario>:<grupo> <nombre_carpeta>
```

## Permisos por defecto: La Máscara `umask`

Cuando creas un nuevo archivo o directorio, el sistema operativo le asigna unos permisos automáticos. Esta configuración no depende de la terminal, sino de la **`umask` (User Mask)** de tu sesión.

La `umask` funciona como una **máscara de sustracción**: en lugar de *añadir* permisos, define qué permisos se le **van a quitar** al valor máximo posible.

### Los Valores Máximos Iniciales

Antes de aplicar la máscara, el sistema operativo parte de un "máximo teórico" de permisos:

* **Directorios (Máximo 777):** Tienen por defecto permisos de lectura, escritura y ejecución (`rwx`) para que puedas entrar en ellos.
* **Archivos (Máximo 666):** Tienen por defecto lectura y escritura (`rw-`). Por seguridad, Linux **nunca** da permisos de ejecución (`x`) automáticos a un archivo nuevo.

### ¿Cómo funciona la resta?

Puedes ver tu máscara actual ejecutando en la terminal:
```bash
$ umask
0022
```
>[!NOTE]
>El primer cero representa permisos especiales, puedes ignorarlo. Quédate con los tres últimos dígitos: `022`.

La matemática que aplica el sistema es una simple resta: **Valor Máximo - Umask = Permiso Final**.

#### Ejemplo con `umask 022`:

```text
  PARA DIRECTORIOS (Máximo 777)         PARA ARCHIVOS (Máximo 666)

    7 7 7  (Máximo total)                  6 6 6  (Máximo total)
  - 0 2 2  (Tu umask)                    - 0 2 2  (Tu umask)
  ────────                                ────────
    7 5 5  (Permiso resultante)            6 4 4  (Permiso resultante)
   (rwxr-xr-x)                            (rw-r--r--)
```

* **Resultado:** Los directorios se crean listos para usarse (`755`), y tus archivos quedan protegidos para que otros usuarios los lean pero no los modifiquen (`644`).

### Cómo cambiarla temporalmente
Si quieres que tus próximos archivos creados sean completamente privados, puedes cambiar la máscara sobre la marcha en tu terminal:

```bash
$ umask 0077
```

>[!WARNING]
>A partir de ese momento, cualquier archivo nuevo tendrá permisos `600` y cualquier directorio `700`.
