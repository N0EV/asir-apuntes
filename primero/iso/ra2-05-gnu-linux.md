# GNU/Linux
GNU/Linux tiene distintas distribuciónes, en nuestro caso escogeremos Ubuntu.

Ubuntu como cualquier SO moderno nos permite interactuar con el mediante dos opciones:

- **GUI** o interfaz gráfica: Escritorio, menús y botones.

- **CLI** o interfaz de comandos: Consola o terminal.

La consola nos permite acceder a un intérprete de órdenes conocido como **Shell**. Cuando escribimos en esta consola un comando esta shell lo interpreta y ejecuta la acción correspondiente.

Para abrir esta consola o terminal puedes o buscar "terminal" o con la convinación de teclas **Ctrl + Alt + T**.

Ubuntu también nos permite abrir consolas de texto sin entorno grafico atraves de las **TTYS** (Consolas Virtuales) para esto podemos cambiar entre ellas con la convinación de teclas **Ctrl + Alt + Fx**, donde x va del 1 al 7.

En unbuntu las F1 y F2 son graficas y las F3-F6 son terminales de texto.

GNU/Linux es Case sensitive por lo que distingue entre mayusculas y minusculas dentro de todo el sistema.

## Interprete de ordenes
El interprete de Ubuntu por defecto es **bash** o bourne again shell. Otros shells son Zsh, Fsh, sh, ksh, etc..., pero bash es el más extendido y compatible con POSIX.

Sus principales caracteristicas son:

- Autocompletado: Al escribir el inicio de un comando o archivo y pulsar la tecla **Tab**, bash completa el texto si es único.

- Historial de comandos: Permite ver y reutilizar comandos anteriores.
    - Flecha hacia arriba o abajo para navegar en el historial.
    - Para mostrarlo usa el comando `history`.
- Estructuras de control para scripting. Admite bucles, condicionales y funciones (if, for, while, case, etc...).
- Alias: permite crear atajos de comandos. Ejemplo: 
```bash  
alias ll=`ls -l`
```

## El prompt en Ubuntu
Al abrir la terminal aparece el **prompt**. Su forma es la siguiente: `usuario@equipo:~$`.

Vamos a desglosarlo para que lo entendamos:
- usuario: nombre del usuario.
- equipo: nombre del equipo (hostname).
- ~: directorio actual (el simbolo `~` significa home del usuario /home/usuario).
- $: significa usuario normal (si aparece `#` significa usuario root).

Y para todas las ordenes siguen el mismo patrón:
`comando [opciones] [argumentos]` Y la salida del programa sera en pantalla a no ser que el programa no produzca una salida explícita.

## Ayuda en GNU/Linux
Este SO ofrece docuemntación muy completa mediante los comandos `man`, `info` y otras herramientas.

### Páginas del manual (man)
Para mostrar la ayudda de este comando usamos `man comando` poniendo en `comando` el comando que queramos buscar en su manual.

La navegación del mismo es simple:
- Flechas, AvPág/RePág para moverse
- /texto para buscar dentro del manual
- n siguiente coincidencia
- N anterior
- g primera línea
- G última línea
- q salir
- h ver ayuda de navegación

### Estructura del comando man
Los manuales están organizados en secciones las cuales son:

| Sección | Contenido |
| :--- | :---- |
| 1 | Programas ejecutables y comandos de usuario|
| 2 | Llamadas al sistema |
| 3 | Llamadas de bibliotecas |
| 4 | Archivos especiales (normalmente en /dev) |
| 5 | Formatos de archivo y convenciones |
| 6 | Juegos |
| 7 | Miscetánea |
| 8 | Administración del sistema |
| 9 | Rutinas del núcleo no estándar |

Ejemplo con estas estructuras:

```bash
man 7 man
```

## Fomato corto y largo de opciones
Muchos comandos permiten opcoiones cortas y largas. Las cortas se usan un solo guion - y las largas dos guiones --. Las opciones cortas generalmente solo son una sola letra mientras que las largas son palabras complejas.

Ejemplos:
```bash
# Opcione cortas
ls -R

# Opciones largas
ls --recursive
```

## Nombre del equipo
Para ver el nombre del equipo usamos el comando `hostname`
tambien `hostanmectl`

Cambiarlo tambien en la ruta `/etc/hosts` dado que es un fichero donde se asociando nombres a direcciones IP.

Para hacer el cambio se hace con el comando:

```bash
sudo hostnamectl set-hostname [nuevo_nombre]
```

## Personalización del entorno (GUI)
Configuración --> Apariencia

Se puede modificar: Fondo de pantalla, tema claro/oscuro, colores, iconos, barra lateral y comportamiento, tipografia, etc...

Opcionalmente instalar otros sistemas de ventanas como gnome-tweaks.

## Optimización del sistema

### Aplicaciones al inicio
Configuración --> Aplicaciones --> Inicio Desactivar las que no se usen esto reduce la carga de trabajo al arrancar el SO.

### Liberación de espacio
En los sistemas GNU/Linux tambien podemos liberar espacio como en Windows. Para ello usamos lo siguiente:

- **apt autoremove:** Elimina automáticamente paquetes que ya no son necesarios. Cuando instalas programas, Ubuntu instala también dependencias. Si después desinstalas el programa principal, pueden quedar dichas dependencias huérfanas.

- **sudo apt clean:** Elimina completamente toda la caché de paquetes descargados. Cuando instalas un programa con apt, ubuntu guarda una copia del paquete .deb en /var/cache/apt/archives/ para futuras instalaciones.

- **sudo apt autoclean:** Similar a `apt clean`, pero solo elimina los paquetes .deb que ya no se pueden descargar es decir versiones antiguas.

Alguna herramienta grafica puede ser `baobab`.

### Optimización de discos
En los HDD GNU/Linux evita la fragmentación de forma natural y en los SSD usa TRIM automáticamente.

Para comprobar TRIM usamos el siguiente comando:
```bash
systemctl status fstrim.timer
```

### Planes de energía
Configuración --> Energía permite ajustar el ahorro de energía, tiempo de suspensión, etc...


### Mantenimiento automático
Ubuntu usa systemd timers que es el equivalente a las tareas programadad de Windows.

comando: `systemctl list-timers`

## Accesibilidad
Configuración --> Accesibilidad

## Configuración de red

### Desde GUI 
Configuración --> Red --> Ethernet/Wifi

### Desde terminal
Ver la ip: `ip a`

Probar conectividad: `ping 8.8.8.8` o `ping google.com`