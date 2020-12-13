
# Table of Contents

1.  [Arch instalation](#org9b1f841)
    1.  [Modificar el repositorio: <code>[6/6]</code>](#org142d7ea)
        1.  [DONE add fonts to repository](#orgde2ecc6)
        2.  [Rofi](#orgece9c7a)
        3.  [quitar emacs.d](#org1983917)
        4.  [agregar .config/doom](#org0983600)
        5.  [Agregar .ncmpcpp](#orgcb0d4b8)
        6.  [Add gtk themes](#orgaf98c87)
    2.  [Scripts: <code>[2/3]</code>](#orgcea7dba)
        1.  [automátizar toda la instalacion y post instalación con excepción de la partición de discos](#org38af487)
        2.  [hacer script para instalar AUR y paquetes automáticamente en arch](#orgec881b0)
        3.  [Hacer master script para agregarlo a los WM: <code>[2/5]</code>](#orge960657)
    3.  [Rise: <code>[3/13]</code>](#org31c967f)
        1.  [bar theme](#org330abc6)
        2.  [Set screen locker](#org4a4f782)
        3.  [Customize Rofi](#org4effc51)
        4.  [Customize lightdm](#org79c5815)
        5.  [Revisar GTK Themes](#org7ebcebd)
        6.  [considerar tint2 como alternativa a polybar](#org43a2275)
        7.  [Customizar grub](#org003c831)
        8.  [install plymouth (plymouth video)](#org9ea435f)
        9.  [launch commands form rofi](#orgd5a56ed)
        10. [Add master script to autorandr.](#org0c7d4d4)
        11. [Clipboard:](#org77ef043)
        12. [Hacer lista de paquetes a instalar en arch](#org1737621)
    4.  [Guía: <code>[1/3]</code>](#org290626c)
        1.  [Cambiar lista ordenada por bullet points](#orgff83a28)
        2.  [configurar bien para convertirla en una página web](#orgd9fbfff)
        3.  [revisar como insertar cursiva](#org019c0a8)
    5.  [Try:](#org721c5de)
        1.  [AUR eDEX-UI](#org2d0f793)
    6.  [Investigar:](#org6cfe4b1)
        1.  [Revisar system-config-printer](#org738fa1c)
        2.  [Revisar pulseaudio y alsamixer](#orge6b3fa4)
        3.  [como hacer transiciones](#org69b2a12)



<a id="org9b1f841"></a>

# PROJ Arch instalation


<a id="org142d7ea"></a>

## TODO Modificar el repositorio: <code>[6/6]</code>


<a id="orgde2ecc6"></a>

### [X] DONE add fonts to repository


<a id="orgece9c7a"></a>

### [X] Rofi


<a id="org1983917"></a>

### [X] quitar emacs.d


<a id="org0983600"></a>

### [X] agregar .config/doom


<a id="orgcb0d4b8"></a>

### [X] Agregar .ncmpcpp


<a id="orgaf98c87"></a>

### [X] Add gtk themes


<a id="orgcea7dba"></a>

## TODO Scripts: <code>[2/3]</code>


<a id="org38af487"></a>

### [X] automátizar toda la instalacion y post instalación con excepción de la partición de discos

1.  DONE after installing arch, mint don&rsquo;t appear in grub

    [fix](https://wiki.archlinux.org/index.php/GRUB#Detecting_other_operating_systems)

2.  DONE keyboard layout no está bien configurado

3.  DONE cambiar todo lo que no sea habitualmente variable para mi a estático

4.  DONE preguntar si quiero montar una partición swap

5.  DONE x11 keyboard layour no funciona por defecto, me carga us layout

    1.  setxkbmap -model pc105 - layout latam me funcionó
    
    2.  comprobar si esto funcina en el script
    
    3.  no funciona en el script porque X server no ha sido iniciado, creo que la mejor opción sería agregar &ldquo;/etc/X11/xorg.conf.d/10-keyboard.conf&rdquo; al repositorio bajo &ldquo;Installation&rdquo; y copiarlo antes de finalizar la instalación

6.  DONE hacer sed a .Xresources me pone literalmente $user en vez del nombre real

7.  DONE Revisa locales antes de reinicar despues de la instalación, verificar si aún existe ingles

    1.  En caso de que no, buscar como mantener el idioma inglés pero poner el teclado en español

8.  DONE añadir instalación de doom emacs y bash


<a id="orgec881b0"></a>

### [X] hacer script para instalar AUR y paquetes automáticamente en arch


<a id="orge960657"></a>

### [ ] Hacer master script para agregarlo a los WM: <code>[2/5]</code>

1.  [ ] Fetch fondos de ser posible.

    1.  [ ] hacer un script que se ejecute diariamente en el servidor para randomizar los fondos
    
    2.  [ ] hacer un script en el (los) clientes para que saquen esos fondos

2.  [X] Lanzar polybar.

3.  [X] Lanzar Picom.

4.  [ ] Havcer más estático el lanzar las bars pero que ejecute la barra correcta

    esto quiere decir distintas versiones de la main/secondary bar dependiendo si se ejecutan en un monitor externo u interno


<a id="org31c967f"></a>

## TODO Rise: <code>[3/13]</code>


<a id="org330abc6"></a>

### [ ] bar theme

1.  [ ] check battery module


<a id="org4a4f782"></a>

### [X] Set screen locker

1.  to wait for idle use xautolock -time *n* -noclose -locker &ldquo;*script*&rdquo;

2.  Light-locker trabaja junto a lightdm

3.  [List of lockers](https://wiki.archlinux.org/index.php/List_of_applications#Screen_lockers)


<a id="org4effc51"></a>

### [ ] Customize Rofi

echo -e &ldquo;Option #1\nOption #2\nOption #3&rdquo; | rofi -dmenu
~/my<sub>script.sh</sub> | rofi -dmenu

1.  for rofi just pipe it the options like:

    [Examples](https://github.com/adi1090x/rofi)

2.  Create something like gnome launcher but nicer


<a id="org79c5815"></a>

### [ ] Customize lightdm

1.  deeping is the green on - nice

2.  slick is the one used by mint - ugly

3.  webkit2s

    1.  aether es el rojo con mucha parafernalia y sidebar para customizar- good one
    
    2.  litarvan es el mejor, parecido a win10
    
    3.  antergos es bastante lindi, parecido a gtk pero más elaborado


<a id="org7ebcebd"></a>

### [X] Revisar GTK Themes


<a id="org43a2275"></a>

### [ ] considerar tint2 como alternativa a polybar


<a id="org003c831"></a>

### [ ] Customizar grub


<a id="org9ea435f"></a>

### [ ] install plymouth [(plymouth video)](https://www.youtube.com/watch?v=eTk2yG1JFsE)


<a id="orgd5a56ed"></a>

### [X] launch commands form rofi


<a id="org0c7d4d4"></a>

### [ ] Add master script to autorandr.


<a id="org77ef043"></a>

### [ ] Clipboard:


<a id="org1737621"></a>

### [ ] Hacer lista de paquetes a instalar en arch


<a id="org290626c"></a>

## TODO Guía: <code>[1/3]</code>


<a id="orgff83a28"></a>

### [ ] Cambiar lista ordenada por bullet points


<a id="orgd9fbfff"></a>

### [ ] configurar bien para convertirla en una página web


<a id="org019c0a8"></a>

### [X] revisar como insertar cursiva


<a id="org721c5de"></a>

## TODO Try:


<a id="org2d0f793"></a>

### TODO AUR eDEX-UI


<a id="org6cfe4b1"></a>

## TODO Investigar:


<a id="org738fa1c"></a>

### DONE Revisar system-config-printer


<a id="orge6b3fa4"></a>

### DONE Revisar pulseaudio y alsamixer

1.  alsa viene con el linux kernel, alsa-utils hay que instalarlo para controlar alsa


<a id="org69b2a12"></a>

### como hacer transiciones

