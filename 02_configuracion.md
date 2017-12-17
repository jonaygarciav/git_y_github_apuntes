# Configurando Git por Primera Vez

Ahora que tienes tenemos _Git_ instalado en nuestro equipo, vamos a configurar algunas opciones de _Git_(estas opciones se pueden cambiar en cualquier momento volviendo a ejecutar los comandos correspondientes).

_Git_ trae una herramienta llamada __git config__ que te permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de __Git__. Cuando con el comando _git config_ usamos la opción _--global_ para definir una propiedad, éstas se almacenan en un fichero de configuración llamado __.gitconfig__ que suele encontrarse en la siguiente ubicación:

* En sistemas Windows el fichero se encuentra en la ubicación _C:\Users\<usuario>\.gitconfig_.
* En sistemas Linux y Mac OS X se encuentra en la ubicación _~/.gitconfig_.

## Identidad

Lo primero que hay que hacer después de instalar _Git_ es establecer tu _nombre de usuario_ y _dirección de correo electrónico_. Esto es importante porque los "commits" de Git usan esta información, y es introducida de manera inmutable en los commits que envías:

```bash
$ git config --global user.name "jonaygarcia"
$ git config --global user.email jonay.garcia@gmail.com
```

De nuevo, solo necesitas hacer esto una vez si especificas la opción --global, ya que _Git_ siempre usará esta información para todo lo que hagas en ese sistema. Si quieres sobrescribir esta información con otro nombre o dirección de correo para proyectos específicos, puedes ejecutar el comando sin la _opción --global_ cuando estés en ese proyecto.

Muchas de las herramientas de interfaz gráfica como [SourceTree](https://www.sourcetreeapp.com/), [GitKraken](https://www.gitkraken.com/), [SmartGit](http://www.syntevo.com/smartgit/) o [eGit](http://www.eclipse.org/egit/) te ayudarán a hacer esto la primera vez que las uses.

## Editor por Defecto

Ahora que nuestra identidad está configurada, podemos elegir el editor de texto por defecto que se utilizará cuando _Git_ necesite que introduzcas un mensaje. Si no indicas nada, _Git_ usa el editor por defecto de tu sistema, que generalmente es _Vim_. Si quieres usar otro editor de texto como _Nano_, puedes hacer lo siguiente:

```bash
$ git config --global core.editor "nano.exe"
```

> __Nota__: _Vim_ y _Nano_ son editores de texto frecuentemente usados por desarrolladores en sistemas basados en _Unix_ como _Linux_ y _Mac_. Si seguiste los pasos del [Anexo I](/anexos/anexo_i.md) para realizar la instalación, no debería hacer falta este paso ya que durante la instalación se configuró para que fuera _Nano_ el editor por defecto.

## Comprobando la Configuración

Si quieres comprobar tu configuración, puedes usar el comando _git config --list_ para mostrar todas las propiedades que _Git_ ha configurado:

```bash
$ git config --list
user.name=jonaygarcia
user.email=jonay.garcia@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
core.editor=nano.exe
...
```

Puede que veas claves repetidas, porque Git lee la misma clave de distintos archivos (/etc/gitconfig y ~/.gitconfig, por ejemplo). En ese caso, Git usa el último valor para cada clave única que ve.

Para ver de qué fichero saca _Git_ cada una de las pripiedades ejecutamos el comando _git config --list --show-origin_:

```bash
$ git config --list --show-origin
file:"C:\\ProgramData/Git/config"       core.symlinks=false
file:"C:\\ProgramData/Git/config"       core.autocrlf=true
file:"C:\\ProgramData/Git/config"       core.fscache=true
file:"C:\\ProgramData/Git/config"       color.diff=auto
file:"C:\\ProgramData/Git/config"       color.status=auto
file:"C:\\ProgramData/Git/config"       color.branch=auto
file:"C:\\ProgramData/Git/config"       color.interactive=true
file:"C:\\ProgramData/Git/config"       help.format=html
file:"C:\\ProgramData/Git/config"       diff.astextplain.textconv=astextplain
file:"C:\\ProgramData/Git/config"       rebase.autosquash=true
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    http.sslbackend=openssl
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    diff.astextplain.textconv=astextplain
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    filter.lfs.clean=git-lfs clean -- %f
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    filter.lfs.smudge=git-lfs smudge -- %f
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    filter.lfs.process=git-lfs filter-process
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    filter.lfs.required=true
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    credential.helper=manager
file:"C:\\Program Files\\Git\\mingw64/etc/gitconfig"    core.editor=nano.exe
file:C:/Users/jonay/.gitconfig  user.email=jonay.garcia@gmail.com
file:C:/Users/jonay/.gitconfig  user.name=jonaygarcia
file:C:/Users/jonay/.gitconfig  filter.lfs.clean=git-lfs clean -- %f
file:C:/Users/jonay/.gitconfig  filter.lfs.smudge=git-lfs smudge -- %f
file:C:/Users/jonay/.gitconfig  filter.lfs.process=git-lfs filter-process
file:C:/Users/jonay/.gitconfig  filter.lfs.required=true
```

También podemos comprobar qué valor utilizará _Git_ para cada clave específica, por ejemplo, para ver el valor de la clave _user.name_:

```bash
$ git config user.name
jonaygarcia
```
