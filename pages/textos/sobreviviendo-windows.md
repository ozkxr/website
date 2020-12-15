---
title: Sobreviviendo Windows
date:  2019-07-16T21:55:00-06:00
---

DRAFT

Por cuestiones de la vida y luego de bastantes años usando Linux, he vuelto a usar Windows como mi sistema operativo principal. Sí, WIndows, ese sistema por el cual tanto he renegado tantos años. Ahora, si bien Windows no es inusable, me ha tocado que hacerle alguno que otro cambio para hacer la experiencia un poco más _a mí modo_.

## El sistema

Es Windows 10. Una versión bastante más bonita que sus predecesoras; simple, moderna, limpia. Pero claro, tuve que hacerle algunas modificaciones.

### Telemetría

Uno de los primeros cambios que hice-y un cambio que recomiendo hacer a __todos__ los usuarios de Windows-es desactivar toda clase de __telemetría__ que viene habilitada por defecto en el sistema. Esto con el fin de hacerlo menos intrusivo, y de paso un poquito más rápido.

La cantidad de _switches_ y botones que hay que mover para dejar todo como tendría que estar no es poca. Pero como no somos pocos los interesados en desactivar todos esto, hay bondadosas personas del internet que hicieron _scripts_ que hacen todo automáticamente, yo me basé en [este post de reddit](https://www.reddit.com/r/Windows10/comments/acwa01/guide_how_to_make_windows_10_less_intrusive_and/).[^1]

Cabe resaltar que, a veces, cuando Windows se actualiza, reactiva algunas de estas configuraciones. Esto hace repetitivo un proceso que, de por sí, ya es tedioso. Y aunque esto se sienta como una batalle interminable, en mi opinion, vale la pena hacer un esfuerzo. La recompensa es un sistema menos intrusivo y más rápido.

### Actualizaciones automáticas

En otro tiempo, también hubiese desactivado las actuaizaciones. Pero las actualizaciones de seguridad son escenciales y creo que es un poco irresponsable no optar por ellas. Ahora bien, prefiero actualizar cuando yo quiero, entonces lo que sí desactivo es el que el sistema haga actualizaciones pre-programadas.

### Cortana y estética

También desactivé a Cortana, la asistente virtual de Windows. Nunca se me ha hecho útil y el sistema corre un poco mejor si está desactivada.

Hice algunos cambios estéticos y de experiencia de usuario, como hacer más pequeños los íconos de la barra de tareas, desabiliar las notificaciones y los _live tiles_ del menú de inicio. También tengo activado el tema oscuro.

## El subsistema

Aquí comienza mi parte favorita.

Esta no es la primera vez que intento usar Windows luego de haber hecho de Linux mi hogar. No es que haya querido dejar Linux, no, no es el caso, pero hay veces-como esta-que uno se ve obligabo.

Y como las otras veces, esta vez-como explico-he querido hacer de Windows un lugar más ameno, para alguien cuyo hogar es Linux. Esta vez tengo corro con más fortuna. Microsoft tiene ya un par de años dandole soporte a algo que a ellos les gusta llamar Windows Subsystem for Linux; un _subsistema_ Linux corriendo en Windows sin la necesidad y pesadez de una máquina virtual.

Sin entrar en mayor detalle aerca de mi epxeriencia con WSL. Basta con decir que obviando un par de pequeñas molestaias sibjetivas, me funciona bastante bien. Hace una diferencia abismal, si la comparamos con las otras veces que he intentado _linuxificar_ Windows con cygwin y mingw.

### Ubuntu

WSL tiene la _amabilidad_ de dar al usuario la capacidad de elegír qué distribución de Linux quiere usar. Lo lógico hubiese sido escoger Arch, la distro que conozco más y con la que he pasado más tiempo. Pero a veces a uno le da por sentar cabeza e irse por lo más estable. Por eso-y antes de arrepentirme-escogí Ubuntu.

Además es la distro _default_ de WSL y mi instinto me dice que es la que menos problemas me dará.

### Emulador de terminal

Para mejorar la experiencia, necesito un emulador de terminal decente. Instalé varios y el que mejor me funcionó por estabilidad y velocidad fue [WSLtty](https://github.com/mintty/wsltty).

WSLtty está basado en mintty y es súper ligero. No tiene algunas _features_ como pestañas y la capacidad de dividir la terminal, pero para cubrir esas necesidades viene bien tmux.

### fish, tmux y sus amigos

#### fish

Mi _shell_ es [fish](http://fishshell.com/). No es compatible con todo. Es más, la mayoría de _scripts_ termino corriendo, pasan siempre por bash. Pero como _shell_ de usuario, es simple de usar y tiene algunas cualidades que en bash solo se consiguen con muchas configuraciones.

#### tmux

Uso tmux para hacer _tiling_ el WSLtty. Para ser honesto, al principio no estaba convencido. No había usado antes tmux porque nunca tuve necesidad. Pero luedo de un par de minutos acostumbrandome a los _hotkeys_, me terminó funciondo mucho mejor de lo que esperaba.

#### VS Code y Vim

Para programar uso dos editores: VS Code y Vim.

Cuando tengo que trabajar en muchos archivos, prefiero VS Code porque no me termino de adaptar a Vim. Antes usaba Atom y Sublime Text. La lentitud de Atom y la culpa por nunca pagar Sublime me hicieron probar VS Code. 

Vim es el editor que uso con más frecuencia. Se me hace más fácil y rápido un editor que funcione en la terminal.

Con Vim he pasado peleando desde la primera vez que lo intenté usar y no me dejaba salir. Creo que es cuestión de perder el miedo y también perseverar. Aún no puedo decir que soy un súper usuario de Vim, pero al menos ya superé esa etapa en la que tenía pesadillas con el editor.

Uso una variante de vim llamada [neovim](https://neovim.io/).

#### Copiar y pegar

Uno de las cosas que tuve que configurar es el _clipboard_, el copy-paste. Digamos que hacer funcionar el _clipboard_ del sistema con la termina, tmux y vim, no tan simple como creí.

1. WSLtty: Marcar el casilla "Atajos Ctrl+Shift+letra" en la sección "Teclas" de las opciones de la terminal.
2. tmux: Habilitar el soporte de mouse e instalar el plugin [tmux-yank](https://github.com/tmux-plugins/tmux-yank).
    ```config
      # Habilitar soporte de mouse
      set -g mouse on
      # Configurar plugins
      set-environment -g TMUX_PLUGIN_MANAGER_PATH '~/.tmux/plugins/'
      set -g @plugin 'tmux-plugins/tmux-yank'
      # Instalar plugins (Esto va al final de el archivo de configuración)
      run -b '~/.tmux/plugins/tpm/tpm'
    ```
3. Vim: Habilitar a el modo `unnamedplus`.
    ```config
      set clipboard+=unnamedplus
    ```
Y con eso, se supone que debería de funcionar el _clipboard_ entre el sistema, la terminal y los programas.

#### Dotfiles

Mis _dotfiles_ de fish, tmux y neovim están en [esta repo de GitHub](https://github.com/ozkxr/dotfiles).

## Fin (?)

Estoy seguro que regresaré a usar Linux como se debe algún día, pero mientras tanto, gracias a WSL, Windows se me está haciendo una experiencia agradable.

[^1]: Es importante hacer un punto de restauración y, si pueden, leer el script.