# Crear un Proyecto Git en Local y Subirlo a GitHub

Suponemos que hemos creado un proyecto en Eclipse llamado _HelloWorld_, este proyecto contiene una carpeta llamada _src/_ que contiene el fichero _HelloWorld.java_ que imprime el mensaje "Hello World!" por consola. Este proyecto se encuentra ubicado en la carepta _C:\Users\%USERNAME%\eclipse-workspace_.

Comprobar los ficheros y directorios de la carpeta del proyecto con el comando "ls":

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld
	$ ls
	bin/  src/

Comprobar los ficheros y directorios de la carpeta incluidos los ficheros ocultos (aquellos que comienzan por ".") del proyecto con el comando "ls -a":
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld
	$ ls -la
	total 10
	drwxr-xr-x 1 Docente 197121   0 dic 14 19:47 ./
	drwxr-xr-x 1 Docente 197121   0 dic 14 19:51 ../
	-rw-r--r-- 1 Docente 197121 303 dic 14 19:47 .classpath
	-rw-r--r-- 1 Docente 197121 386 dic 14 19:47 .project
	drwxr-xr-x 1 Docente 197121   0 dic 14 19:47 .settings/
	drwxr-xr-x 1 Docente 197121   0 dic 14 19:50 bin/
	drwxr-xr-x 1 Docente 197121   0 dic 14 19:50 src/

Listar los ficheros de la carpeta "src/":

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld
	$ ls src/
	HelloWorld.java

Crear un repositorio Git dentro de la carpeta del proyecto con el comando "git init":
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld
	$ git init
	Initialized empty Git repository in C:/Users/Docente/eclipse-workspace/HelloWorld/.git/

Hacer un "git status" para comprobar los ficheros que puedo añadir a control de versiones:
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git status
	On branch master

	No commits yet

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

			.classpath
			.project
			.settings/
			bin/
			src/

	nothing added to commit but untracked files present (use "git add" to track)

Sólo me interesa quedarme con la carpeta "src/", el resto de ficheros y directorios me interesa obviarlos, para ello, utilizar el editor de texto "nano" para crear un fichero llamado ".gitignore" y añado los ficheros y carpetas que quiero obviar:

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ nano .gitignore

	(Editamos el fichero)

Comandos del editor "nano":

* Para guardar cambios: CTRL + O, y luego ENTER.
* Para salir de nano:   CTRL + X.
* Para movernos por las diferentes lineas del fichero usamos los cursores.

Mostrar el contenido del fichero ".gitignore" con el comando "cat .gitignore":

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ cat .gitignore

	.classpath
	.project
	.settings/
	bin/

Hacer un "git status" y comprobar que sólo vemos la carpeta "src/" y el fichero ".gitignore". Los ficheros y directorios que se encuentran en el fichero ".gitignore" son ignorados por _Git_:

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git status
	On branch master

	No commits yet

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

			.gitignore
			src/

	nothing added to commit but untracked files present (use "git add" to track)

Añadir los ficheros al _Stage Area_ para poder hacer el commit posteriormente con el comando "git add .":
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git add .
	warning: LF will be replaced by CRLF in .gitignore.
	The file will have its original line endings in your working directory.
	
Hacer un "git status" y vemos que se ponen en color verde y el mensaje cambia:
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git status
	On branch master

	No commits yet

	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)

			new file:   .gitignore
			new file:   src/HelloWorld.java

Ya estamos listos para guardar los cambios, para ello, hacer un "git commit":
			
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git commit -m "Commit inicial"

	*** Please tell me who you are.

	Run

	  git config --global user.email "you@example.com"
	  git config --global user.name "Your Name"

	to set your account's default identity.
	Omit --global to set the identity only in this repository.

	fatal: unable to auto-detect email address (got 'Docente@CIP000342.(none)')

Da un error porque cuando hacemos un commit, Git guarda la información de la persona que ha realizado los cambios (usuario y email) (esta tarea sólo hay que hacerla una vez):

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git config --global user.email "jonay.garcia@gmail.com"

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git config --global user.name "jonaygarcia"

Ver si hemos añadido correctamente la información del usuario (usuario y email) con el comando "git config --list":

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git config --list
	...
	user.email=jonay.garcia@gmail.com
	user.name=jonaygarcia
	...

Intentamos hacer de nuevo el commit, esta vez no nos da ningún problema:
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git commit -m "Commit inicial"
	[master (root-commit) c0b7c11] Commit inicial
	 2 files changed, 15 insertions(+)
	 create mode 100644 .gitignore
	 create mode 100644 src/HelloWorld.java

	 
Para ver el listado de commits que hemos hecho ejecutamos el comando "git log":
	 
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git log
	commit c0b7c1126c065e359a21038e800336ed434b9332 (HEAD -> master)
	Author: jonaygarcia <jonay.garcia@gmail.com>
	Date:   Thu Dec 14 20:57:21 2017 +0000

		Commit inicial


Desde el navegador abrimos la página web de GitHub y creamos un nuevo repositorio llamado "HelloWorld", la URL del proyecto creado es:

	https://github.com/jonaygarcia/helloworld.git

Configuramos nuestro proyecto indicándole la ruta del repositorio de GitHub donde vamos a subir el código (esto sólo se hace 1 vez por proyecto):
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git remote add origin https://github.com/jonaygarcia/helloworld.git

Subimos el código a GitHub:
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git push -u origin master
	Counting objects: 5, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (5/5), 457 bytes | 228.00 KiB/s, done.
	Total 5 (delta 0), reused 0 (delta 0)
	To https://github.com/jonaygarcia/helloworld.git
	 * [new branch]      master -> master
	Branch 'master' set up to track remote branch 'master' from 'origin'.
	
Recargar la página web del proyecto en GitHub y deberíamos ver el código fuente.

Hemos introducido un segundo cambio. Ahora hemos modificado el fichero "src/HelloWorld.java" para que muestre otro mensaje por pantalla. Si hacemos un "git status" nos indica que ese fichero tiene cambios que no han sido commiteados:

	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git status
	On branch master
	Your branch is up to date with 'origin/master'.

	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git checkout -- <file>..." to discard changes in working directory)

			modified:   src/HelloWorld.java

	no changes added to commit (use "git add" and/or "git commit -a")

	
Añadir el fichero al Stage Area antes de ser commiteado con el comando "git add .":
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git add .
	
Guardar los cambios:
	
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git commit -m "Se añade nuevo mensaje por pantalla"
	[master a7aee66] Se añade nuevo mensaje por pantalla
	 1 file changed, 2 insertions(+), 1 deletion(-)
	 
Ver un listado de los commits que hemos hecho con un "git log":
	 
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git log
	commit a7aee663eb2411040373b2c3e434d26b6915bd4e (HEAD -> master)
	Author: jonaygarcia <jonay.garcia@gmail.com>
	Date:   Thu Dec 14 21:03:56 2017 +0000

		Se añade nuevo mensaje

	commit c0b7c1126c065e359a21038e800336ed434b9332 (origin/master)
	Author: jonaygarcia <jonay.garcia@gmail.com>
	Date:   Thu Dec 14 20:57:21 2017 +0000

		Commit inicial

Subir los cambios a GitHub:
		
	Docente@CIP000342 MINGW64 ~/eclipse-workspace/HelloWorld (master)
	$ git push origin master
	Counting objects: 4, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (4/4), 385 bytes | 385.00 KiB/s, done.
	Total 4 (delta 1), reused 0 (delta 0)
	remote: Resolving deltas: 100% (1/1), completed with 1 local object.
	To https://github.com/jonaygarcia/helloworld.git
	   c0b7c11..a7aee66  master -> master