
## Renombrar y Eliminar Ficheros o Directorios

## Eliminar Archivos

Para eliminar archivos de _Git_, debemos eliminarlos de tus archivos rastreados (o mejor dicho, eliminarlos del área de preparación) y luego confirmar. Para ello existe el comando _git rm_, que además elimina el archivo de tu directorio de trabajo de manera que no aparezca la próxima vez como un archivo no rastreado.

Si simplemente eliminamos el archivo de tu directorio de trabajo, aparecerá en la sección “Changes not staged for commit” (esto es, sin preparar) en la salida de _git status_:

```bash
$ rm PROJECTS.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
(use "git add/rm <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)

deleted: PROJECTS.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Ahora, si ejecutamos _git rm_, entonces se prepara la eliminación del archivo:

```bash
$ git rm PROJECTS.md
rm 'PROJECTS.md'
$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)

deleted: PROJECTS.md
```

Con la próxima confirmación, el archivo habrá desaparecido y no volverá a ser rastreado. Si modificamos el archivo y ya lo habíamos añadido al índice, tendrás que forzar su eliminación con la opción -f. Esta propiedad existe por seguridad, para prevenir que elimines accidentalmente datos que aun no han sido guardados como una instantánea y que por lo tanto no podrás recuperar luego con _Git_.

Otra cosa que puedas querer hacer es mantener el archivo en tu directorio de trabajo pero eliminarlo del área de preparación. En otras palabras, quisieras mantener el archivo en tu disco duro pero sin que _Git_ lo siga rastreando. Esto puede ser particularmente útil si olvidaste añadir algo en tu archivo _.gitignore_ y lo preparaste accidentalmente. Para hacerlo, utiliza la opción _--cached_:

```bash
$ git rm --cached README
```

Al comando _git rm_ podemos pasarle archivos y directorios, lo que significa que puedes hacer cosas como:

```bash
$ git rm log/\*.log
```

Fíjate en la barra invertida (\) antes del asterisco *. Esto es necesario porque Git hace su propia expansión de nombres de archivo, aparte de la expansión hecha por tu terminal. Este comando elimina todos los archivo que tengan la extensión .log dentro del directorio log/. O también puedes hacer algo como:

```bash
$ git rm \*~
```

Este comando elimina todos los archivos que acaben con ~.

## Cambiar el Nombre de los Archivos

Al contrario que muchos sistemas VCS, _Git_ no rastrea explícitamente los cambios de nombre en archivos. Si renombras un archivo en _Git_, no se guardará ningún metadato que indique que renombraste el archivo.

Para esto, _Git_ tiene el comando _git mv_. Si queremos renombrar un archivo en _Git_, podemos ejecutar lo siugiente:

```bash
$ git mv file_from file_to
```

De hecho, si ejecutamos algo como eso y vemos el estado, veremos que _Git_ lo considera como un renombramiento de archivo:

```bash
$ git mv README.md README

$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)

renamed: README.md -> README
```

Sin embargo, eso es equivalente a ejecutar algo como esto:

```bash
$ mv README.md README
$ git rm README.md
$ git add README
```

_Git_ se da cuenta que es un renombramiento implícito, así que no importa si renombramos el archivo de esa manera o a través del comando _mv_. La única diferencia real es que _mv_ es un solo comando en vez de tres.