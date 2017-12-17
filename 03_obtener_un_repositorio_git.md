# Obteniendo un Repositorio Git

Se puede obtener un proyecto _Git_ de dos maneras. La primera es tomar un proyecto o directorio existente e importarlo en _Git_. La segunda es clonar un repositorio existente en Git desde otro servidor como _GitHub_.

## Inicializando un Repositorio en un Directorio Existente

Si empezamos a seguir un proyecto existente en _Git_, debemos ir al directorio del proyecto y usar el siguiente comando:

```bash
$ git init
```

Esto crea un subdirectorio nuevo llamado _.git_, el cual contiene todos los archivos necesarios del repositorio y donde irá guardando todos los cambios que se vayan commiteando. En este estado todavía no hay nada en nuestro proyecto que esté bajo seguimiento.

Para empezar a controlar versiones de archivos existentes (a diferencia de un directorio vacío), hay que comenzar el seguimiento de esos archivos y hacer una confirmación inicial (primer commit). Esto se hace con unos pocos comandos: __git add__ para especificar qué archivos quieres controlar, seguido de un __git commit__ para confirmar los cambios:

```bash
$ git add *.java
$ git add README
$ git commit -m 'Commit inicial'
```

Veremos lo que hacen estos comandos más adelante. En este momento, tienes un repositorio de _Git_ con archivos bajo seguimiento y una confirmación inicial (primer commit).

## Clonando un Repositorio Existente

Si deseas obtener una copia de un repositorio Git existente, por ejemplo, un proyecto en el que te gustaría contribuir que esté alojado en _GitHub_, necesitamos ejecutar el comando __git clone__. La sintaxis para clonar un repositorio es _git clone [url]_. Por ejemplo, si quieres clonar un repositorio de una aplicaicón java sencilla que tengo yo en mi cuenta _GitHub_:

```bash
$ git clone https://github.com/jonaygarcia/java_helloworld.git
```

Esto crea un directorio llamado _java_helloworld_, inicializa un directorio _.git_ en su interior, descarga toda la información de ese repositorio y saca una copia de trabajo de la última versión. Si te metes en el directorio _java_helloworld_, verás que están los archivos del proyecto listos para ser utilizados. Si quieres clonar el repositorio a un directorio con otro nombre que no sea _java_helloworld_, puedes especificarlo con la siguiente opción de línea de comandos:

````bash
$ git clone https://github.com/jonaygarcia/java_helloworld.git helloworld
```

Ese comando hace lo mismo que el anterior, pero el directorio de destino se llamará _helloworld_.

Git permite usar distintos protocolos de transferencia. El ejemplo anterior usa el protocolo https://, pero también se puede utilizar git:// que utiliza el protocolo de transferencia SSH.


