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