# Instalación de Git

## Instalación sobre Windows
Ir a la dirección web [https://git-scm.com/](https://git-scm.com/) y descargar el ejecutable de Git donde pone _Download 2.15.1 for Windows:

![](/assets/img/anexo_i/01.png)

> __Nota__: Durante la realización de este tutorial la última versión de _Git_ era la  _2.15.1_.

A continuación la descarga se inicia automáticamente:

![](/assets/img/anexo_i/02.png)

En caso de que no se inicia automáticamente, pulsar en la opción _64-bit Git for Windows Setup_:

Esto nos descarga un fichero llamado _Git-2.15.1.2-64-bit.exe_ lo ejecutamos y nos abrirá un _Asistente_.

En esta ventana muestra información sobre la licencia de _Git_, pulsamos el bótón _Next >_:

![](/assets/img/anexo_i/03.png)

En esta ventana muestra información sobre la carpeta en el sistema donde se va a instalar _Git_, por defecto es _C:\Program Files\Git_. Lo dejamos como está y pulsamos el botón _Next >_:

![](/assets/img/anexo_i/04.png)

En esta ventana muestra un listado de los componentes que van a ser instalados:

![](/assets/img/anexo_i/05.png)

En esta ventana muestra el nombre de la carpeta que se creará en el _Menu Inicio_. Lo dejamos como está y pulsamos _Next >_:

![](/assets/img/anexo_i/06.png)

Seleccionamos el editor _Nano_ como editor por defecto, ya que es más sencillo de usar que el _Vim_. Pulsamos el botón _Next >_:

![](/assets/img/anexo_i/07.png)

En la siguiente ventana, la opción __Use Git from the Windows Command Prompt__ permite usar el comando _Git_, tanto de la consola _Git Bash_ como de un _Símbolo de Sistema_. Dejamos marcada la opción por defecto y pulsamos el botón _Next >_:

![](/assets/img/anexo_i/08.png)

La opción __Use the OpenSSL library__ indica que utilizará la herramienta OpenSSL para validar los certificados de servidor cuando en utilicemos _GIT_ con autenticación a través de claves públicas SSH. Dejamos marcada la opción por defecto y pulsamos el botón _Next >_:

![](/assets/img/anexo_i/09.png)

La opción __Checkout Windows-style, commit Unix-style line endings__ convierte los saltos de línea __LF__ en __CRLF__. Los saltos de línea en sistemas Unix se identifican con el código de control _LF (salto de línea)_, sin embargo, los saltos de línea en sistemas Windows se identifican con dos códigos de control: __CR (retorno de carro)__ y __LF (salto de línea)__. Se hace esto para que los ficheros que guarde el _Git_ sean compatibles con el mayor número de plataformas: Windows, Linux, Unix, ... Dejamos marcada la opción por defecto y pulsamos el botón _Next >_:

![](/assets/img/anexo_i/10.png)

En la siguiente ventana, la opción __Use MinTTY__ indica que la consola _Git Bash_ usará _MinTTY_ como emulador. Dejamos marcada la opción por defecto y pulsamos el botón _Next >_:

![](/assets/img/anexo_i/11.png)

En esta ventana se añaden configuraciones extra como puede ser _habilitar el sistema de cachés_ o _habilitar el gestor de credenciales Git_, una manera segura de guardar en nuestro equipo las credenciales de sitios como GitHub. Dejamos las opciones marcadas por defecto y pulsamos la tecla _Next >_:

![](/assets/img/anexo_i/12.png)

¡Listo! Ya tenemos instalado _Git_ en nuestro equipo. Ahora marcamos la opción _Launch Git Bash_ para que abra una terminal _Git Bash_:

![](/assets/img/anexo_i/13.png)

Ejecutamos el comando _git --version_, si todo va bien debería devolver la versión de _Git_ que acabamos de instalar.

![](/assets/img/anexo_i/14.png)

## Instalación sobre Mac OSX

Para instalar _Git_ en un sistema _MaC OS X_, lo mejor es instalarlo utilizando el gestor de paquetes [Homebrew](https://brew.sh/index_es.html).

Una vez instalado _Homebrew_, para instalar _Git_:

```bash
$ brew install git
```

## Instalación sobre Linux

En sistemas _Linux_ basados en paquetes _.deb_ como _Ubuntu_:

```bash
$ sudo apt-get install git
```
