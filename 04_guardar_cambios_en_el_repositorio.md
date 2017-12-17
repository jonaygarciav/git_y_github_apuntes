# Guardando Cambios en el Repositorio

Ya tenemos un repositorio Git y un copia de trabajo de los archivos de dicho proyecto. El siguiente paso es realizar algunos cambios y confirmar instantáneas de esos cambios en el repositorio cada vez que el proyecto alcance un estado que quieras conservar.

Recuerda que cada archivo de tu repositorio puede tener dos estados: __rastreados__ y __sin rastrear__:

* Los __archivos rastreados__ (_tracked files_ en inglés) son todos aquellos archivos que estén bajo control de versiones.
* Los __archivos sin rastrear__ son archivos de nuestro directorio de trabajo que no está aún bajo control de versiones y que no están en el área de preparación (staging area).

Cuando editas un archivo, Git los ve como _modificado_, pues ha sido cambiado desde su último commit. Luego preparas este archivo modificado y finalmente confirmas todos los cambios preparados, y repitimos el ciclo.

![](/assets/img/04_guardando_cambios_en_el_repositorio/01.png)

## Revisando el Estado de tus Archivos

La herramienta principal para determinar qué archivos están en qué estado es el comando __git status__. Si ejecutamos este comando inmediatamente después de clonar un repositorio, veremos algo como esto:

````bash
$ git status
On branch master
nothing to commit, working directory clean
```

Esto significa que tienes un directorio de trabajo limpio, en otras palabras, que no hay archivos rastreados ni modificados. Además, _Git_ no encuentra ningún archivo sin rastrear, de lo contrario aparecerían listados aquí. Finalmente, el comando te indica en qué rama estás y te informa que no ha variado con respecto a la misma rama en el servidor. Por ahora, la rama siempre será “master”, que es la rama por defecto.

Añadimos un archivo al proyecto, un archivo _README.md_. Si el archivo no existía antes, y ejecutas _git status_, verás el archivo sin rastrear de la siguiente manera:

```bash
$ echo 'Mi Proyecto' > README.md
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README.md

nothing added to commit but untracked files present (use "git add" to track)
```    

Se puede ver que el archivo _README.md_ está sin rastrear porque aparece debajo del encabezado “Untracked files” (“Archivos no rastreados” en inglés) en la salida. Sin rastrear significa que _Git_ ve archivos que no tenías en el commit anterior. _Git_ no los incluirá en tu próximo commit a menos que se lo indiques explícitamente. Se comporta así para evitar incluir accidentalmente archivos binarios o cualquier otro archivo que no quieras incluir. Como queremos incluir _README.md_, debemos empezar a rastrearlo.

## Rastrear Archivos Nuevos

Para comenzar a rastrear un archivo debemosusar el comando __git add__. Para comenzar a rastrear el archivo _README.md_, ejecutamos el siguiente comando:

```bash
$ git add README.md
```

Ahora si vuelves a ver el estado del proyecto, verás que el archivo _README.md_ está siendo rastreado y está preparado para ser confirmado:

```bash
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README.md
```

Podemos ver que está siendo rastreado porque aparece luego del encabezado “Cambios a ser confirmados” (“Changes to be committed” en inglés). Si confirmamos en este punto, se guardará en el historial la versión del archivo correspondiente al instante en que ejecutaste _git add_. Anteriormente cuando ejecutamos _git init_, ejecutamos posteiormente _git add (files)_, lo que inició el rastreo de archivos en nuestro directorio. El comando _git add_ puede recibir tanto una ruta de archivo como de un directorio; si es de un directorio, el comando añade recursivamente los archivos que están dentro de él.

## Preparar Archivos Modificados

Cambiamos un archivo que ya esté rastreado (se haya hecho al menos un commit). Si cambias el archivo rastreado llamado “CONTRIBUTING.md” y luego ejecutas el comando _git status_, verás algo parecido a esto:

```bash
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

El archivo “CONTRIBUTING.md” aparece en una sección llamada “Changes not staged for commit” (“Cambios no preparado para confirmar” en inglés), que significa que existe un archivo rastreado que ha sido modificado en el directorio de trabajo pero que aun no está preparado. Para prepararlo, ejecutamos el comando _git add_. _git add_ es un comando que cumple varios propósitos, se usa para empezar a rastrear archivos nuevos, preparar archivos, y hacer otras cosas como marcar como resuelto archivos en conflicto por combinación. Es más útil verlo como un comando para “añadir este contenido a la próxima confirmación” mas que para “añadir este archivo al proyecto”. Ejecutamos _git add_ para preparar el archivo “CONTRIBUTING.md” y luego ejecutamos _git status_:

```bash
$ git add CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README.md
    modified:   CONTRIBUTING.md
```

Ambos archivos están preparados y formarán parte de nuestra próxima confirmación (commit). En este momento, supongamos que debemos hacer un pequeño cambio en el fichero _CONTRIBUTING.md_ antes de confirmarlo. Abrimos de nuevo el archivo, lo cambiamos y ahora está listos para confirmar. Sin embargo, si ejecutamos _git status_ una vez más:

```bash
$ vim CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README.md
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

Ahora _CONTRIBUTING.md_ aparece como preparado y como no preparado. ¿Cómo es posible? Resulta que Git prepara un archivo de acuerdo al estado que tenía cuando ejecutamos el comando _git add_. Si confirmamos ahora, se confirmará la versión de _CONTRIBUTING.md_ que tenías la última vez que ejecutaste _git add_ y no la versión que ves ahora en tu directorio de trabajo al ejecutar _git commit_. Si modificas un archivo luego de ejecutar _git add_, deberás ejecutar _git add_ de nuevo para preparar la última versión del archivo:

```bash
$ git add CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README.md
    modified:   CONTRIBUTING.md


## Ignorar Archivos

A veces, tendremos algún tipo de archivo que no queremos que _Git_ añada automáticamente o  que ni siquiera queremos que aparezca como _no rastreado_. Este suele ser el caso de archivos generados automáticamente como trazas o archivos creados por un sistema de construcción de proyectos como Maven, o un IDE como Eclipse. En estos casos, puedes crear un archivo llamado __.gitignore__ que liste patrones a considerar. Este es un ejemplo de un archivo _.gitignore_:

```bash
$ cat .gitignore
*.class
bin/
```

* La primera línea le indica a _Git_ que ignore cualquier archivo cuya extensión sea ".class", archivos compilados que no nos interesa rastrear.
* La segunda línea le indica a _Git_ que ignore la carpeta _bin/_ y todos los ficheros y subdirectorios que se encuentren en ella.

> __Nota__: Crear un archivo __.gitignore__ antes de comenzar a trabajar es generalmente una buena idea pues así evitas confirmar accidentalmente archivos que en realidad no quieres incluir en tu repositorio Git.

A continuación puedes ver algunos ejemplos de reglas que se pueden aplicar al archivo _.gitignore_:

```bash
# ignora los archivos terminados en .a
*.a

# pero no lib.a, aun cuando había ignorado los archivos terminados en .a en la linea anterior
!lib.a

# ignora unicamente el archivo TODO de la raiz, no subdir/TODO
/TODO

# ignora todos los archivos del directorio build/
build/

# ignora doc/notes.txt, pero este este fichero no lo ignora: doc/server/arch.txt
doc/*.txt

# ignora todos los archivos .txt del directorio doc/
doc/**/*.txt
```

> __Nota__: _GitHub_ mantiene una extensa lista de archivos _.gitignore_ adecuados a docenas de proyectos y lenguajes en la URL [https://github.com/github/gitignore](https://github.com/github/gitignore) en caso de que queramos tener un punto de partida para nuestro proyecto.

# Ver los Cambios Preparados y No Preparados

Si el comando git status es muy impreciso para ti - quieres ver exactamente que ha cambiado, no solo cuáles archivos lo han hecho - puedes usar el comando git diff. Hablaremos sobre git diff más adelante, pero lo usarás probablemente para responder estas dos preguntas: ¿Qué has cambiado pero aun no has preparado? y ¿Qué has preparado y está listo para confirmar? A pesar de que git status responde a estas preguntas de forma muy general listando el nombre de los archivos, git diff te muestra las líneas exactas que fueron añadidas y eliminadas, es decir, el parche.

Supongamos que editas y preparas el archivo README de nuevo y luego editas CONTRIBUTING.md pero no lo preparas. Si ejecutas el comando git status, verás algo como esto:

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
Para ver qué has cambiado pero aun no has preparado, escribe git diff sin más parámetros:

$ git diff
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
 Please include a nice description of your changes when you submit your PR;
 if we have to read the whole diff to figure out why you're contributing
 in the first place, you're less likely to get feedback and have your change
-merged in.
+merged in. Also, split your changes into comprehensive chunks if you patch is
+longer than a dozen lines.

 If you are starting to work on a particular area, feel free to submit a PR
 that highlights your work in progress (and note in the PR title that it's
Este comando compara lo que tienes en tu directorio de trabajo con lo que está en el área de preparación. El resultado te indica los cambios que has hecho pero que aun no has preparado.

Si quieres ver lo que has preparado y será incluido en la próxima confirmación, puedes usar git diff --staged. Este comando compara tus cambios preparados con la última instantánea confirmada.

$ git diff --staged
diff --git a/README b/README
new file mode 100644
index 0000000..03902a1
--- /dev/null
+++ b/README
@@ -0,0 +1 @@
+My Project
Es importante resaltar que al llamar a git diff sin parámetros no verás los cambios desde tu última confirmación - solo verás los cambios que aun no están preparados. Esto puede ser confuso porque si preparas todos tus cambios, git diff no te devolverá ninguna salida.

Pasemos a otro ejemplo, si preparas el archivo CONTRIBUTING.md y luego lo editas, puedes usar git diff para ver los cambios en el archivo que están preparados y los cambios que no lo están. Si nuestro ambiente es como este:

$ git add CONTRIBUTING.md
$ echo 'test line' >> CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
Puedes usar git diff para ver qué está sin preparar

$ git diff
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 643e24f..87f08c8 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -119,3 +119,4 @@ at the
 ## Starter Projects

 See our [projects list](https://github.com/libgit2/libgit2/blob/development/PROJECTS.md).
+# test line
y git diff --cached para ver que has preparado hasta ahora (--staged y --cached son sinónimos):

$ git diff --cached
diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
index 8ebb991..643e24f 100644
--- a/CONTRIBUTING.md
+++ b/CONTRIBUTING.md
@@ -65,7 +65,8 @@ branch directly, things can get messy.
 Please include a nice description of your changes when you submit your PR;
 if we have to read the whole diff to figure out why you're contributing
 in the first place, you're less likely to get feedback and have your change
-merged in.
+merged in. Also, split your changes into comprehensive chunks if you patch is
+longer than a dozen lines.

 If you are starting to work on a particular area, feel free to submit a PR
 that highlights your work in progress (and note in the PR title that it's
Note
Git Diff como Herramienta Externa
A lo largo del libro, continuaremos usando el comando git diff de distintas maneras. Existe otra forma de ver estas diferencias si prefieres utilizar una interfaz gráfica u otro programa externo. Si ejecutas git difftool en vez de git diff, podrás ver los cambios con programas de este tipo como Araxis, emerge, vimdiff y más. Ejecuta git difftool --tool-help para ver qué tienes disponible en tu sistema.

Confirmar tus Cambios
Ahora que tu área de preparación está como quieres, puedes confirmar tus cambios. Recuerda que cualquier cosa que no esté preparada - cualquier archivo que hayas creado o modificado y que no hayas agregado con git add desde su edición - no será confirmado. Se mantendrán como archivos modificados en tu disco. En este caso, digamos que la última vez que ejecutaste git status verificaste que todo estaba preparado y que estás listos para confirmar tus cambios. La forma más sencilla de confirmar es escribiendo git commit:

$ git commit
Al hacerlo, arrancará el editor de tu preferencia. (El editor se establece a través de la variable de ambiente $EDITOR de tu terminal - usualmente es vim o emacs, aunque puedes configurarlo con el editor que quieras usando el comando git config --global core.editor tal como viste en Inicio - Sobre el Control de Versiones).

El editor mostrará el siguiente texto (este ejemplo corresponde a una pantalla de Vim):

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#	new file:   README
#	modified:   CONTRIBUTING.md
#
~
~
~
".git/COMMIT_EDITMSG" 9L, 283C
Puedes ver que el mensaje de confirmación por defecto contiene la última salida del comando git status comentada y una línea vacía encima de ella. Puedes eliminar estos comentarios y escribir tu mensaje de confirmación, o puedes dejarlos allí para ayudarte a recordar qué estás confirmando. (Para obtener una forma más explícita de recordar qué has modificado, puedes pasar la opción -v a git commit. Al hacerlo se incluirá en el editor el diff de tus cambios para que veas exactamente qué cambios estás confirmando.) Cuando sales del editor, Git crea tu confirmación con tu mensaje (eliminando el texto comentado y el diff).

Otra alternativa es escribir el mensaje de confirmación directamente en el comando commit utilizando la opción -m:

$ git commit -m "Story 182: Fix benchmarks for speed"
[master 463dc4f] Story 182: Fix benchmarks for speed
 2 files changed, 2 insertions(+)
 create mode 100644 README
¡Has creado tu primera confirmación (o commit)! Puedes ver que la confirmación te devuelve una salida descriptiva: indica cuál rama has confirmado (master), que checksum SHA-1 tiene el commit (463dc4f), cuántos archivos han cambiado y estadísticas sobre las líneas añadidas y eliminadas en el commit.

Recuerda que la confirmación guarda una instantánea de tu área de preparación. Todo lo que no hayas preparado sigue allí modificado; puedes hacer una nueva confirmación para añadirlo a tu historial. Cada vez que realizas un commit, guardas una instantánea de tu proyecto la cual puedes usar para comparar o volver a ella luego.

Saltar el Área de Preparación
A pesar de que puede resultar muy útil para ajustar los commits tal como quieres, el área de preparación es a veces un paso más complejo a lo que necesitas para tu flujo de trabajo. Si quieres saltarte el área de preparación, Git te ofrece un atajo sencillo. Añadiendo la opción -a al comando git commit harás que Git prepare automáticamente todos los archivos rastreados antes de confirmarlos, ahorrándote el paso de git add:

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git commit -a -m 'added new benchmarks'
[master 83e38c7] added new benchmarks
 1 file changed, 5 insertions(+), 0 deletions(-)
Fíjate que en este caso no fue necesario ejecutar git add sobre el archivo CONTRIBUTING.md antes de confirmar.

Eliminar Archivos
Para eliminar archivos de Git, debes eliminarlos de tus archivos rastreados (o mejor dicho, eliminarlos del área de preparación) y luego confirmar. Para ello existe el comando git rm, que además elimina el archivo de tu directorio de trabajo de manera que no aparezca la próxima vez como un archivo no rastreado.

Si simplemente eliminas el archivo de tu directorio de trabajo, aparecerá en la sección “Changes not staged for commit” (esto es, sin preparar) en la salida de git status:

$ rm PROJECTS.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    PROJECTS.md

no changes added to commit (use "git add" and/or "git commit -a")
Ahora, si ejecutas git rm, entonces se prepara la eliminación del archivo:

$ git rm PROJECTS.md
rm 'PROJECTS.md'
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    deleted:    PROJECTS.md
Con la próxima confirmación, el archivo habrá desaparecido y no volverá a ser rastreado. Si modificaste el archivo y ya lo habías añadido al índice, tendrás que forzar su eliminación con la opción -f. Esta propiedad existe por seguridad, para prevenir que elimines accidentalmente datos que aun no han sido guardados como una instantánea y que por lo tanto no podrás recuperar luego con Git.

Otra cosa que puedas querer hacer es mantener el archivo en tu directorio de trabajo pero eliminarlo del área de preparación. En otras palabras, quisieras mantener el archivo en tu disco duro pero sin que Git lo siga rastreando. Esto puede ser particularmente útil si olvidaste añadir algo en tu archivo .gitignore y lo preparaste accidentalmente, algo como un gran archivo de trazas a un montón de archivos compilados .a. Para hacerlo, utiliza la opción --cached:

$ git rm --cached README
Al comando git rm puedes pasarle archivos, directorios y patrones glob. Lo que significa que puedes hacer cosas como

$ git rm log/\*.log
Fíjate en la barra invertida (\) antes del asterisco *. Esto es necesario porque Git hace su propia expansión de nombres de archivo, aparte de la expansión hecha por tu terminal. Este comando elimina todos los archivo que tengan la extensión .log dentro del directorio log/. O también puedes hacer algo como:

$ git rm \*~
Este comando elimina todos los archivos que acaben con ~.

Cambiar el Nombre de los Archivos
Al contrario que muchos sistemas VCS, Git no rastrea explícitamente los cambios de nombre en archivos. Si renombras un archivo en Git, no se guardará ningún metadato que indique que renombraste el archivo. Sin embargo, Git es bastante listo como para detectar estos cambios luego que los has hecho - más adelante, veremos cómo se detecta el cambio de nombre.

Por esto, resulta confuso que Git tenga un comando mv. Si quieres renombrar un archivo en Git, puedes ejecutar algo como

$ git mv file_from file_to
y funcionará bien. De hecho, si ejecutas algo como eso y ves el estatus, verás que Git lo considera como un renombramiento de archivo:

$ git mv README.md README
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
Sin embargo, eso es equivalente a ejecutar algo como esto:

$ mv README.md README
$ git rm README.md
$ git add README
Git se da cuenta que es un renombramiento implícito, así que no importa si renombras el archivo de esa manera o a través del comando mv. La única diferencia real es que mv es un solo comando en vez de tres - existe por conveniencia. De hecho, puedes usar la herramienta que quieras para renombrar un archivo y luego realizar el proceso rm/add antes de confirmar.