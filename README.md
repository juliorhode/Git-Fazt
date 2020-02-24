# Git
Git es un sistema de control de versiones el cual mantiene un orden cronológico de los cambios que vayamos haciendo en nuestro proyecto.

En Git contamos con tres (3) etapas de estados:
1. **working directory**  
    Es donde estas tranajando con los archivos normalmente.
2. **staging area**  
    Esta area es donde se agregan los archivos para prepararlos al guardado definitivo.
3. **repository**  
    Aqui ya estan almacenados de forma definitiva.


- **git init**  
  Indicamos a nuestro proyecto que vamos usar git.
- **git add <file>**  
  Pasamos los archivos del estado **1 al estado 2**.
- **git status**  
  Para ver el estado de los archivos.
- **git commit**  
  Para pasar los archivos del estado **2 al 3**.
- **git push**  
  Para subir los archivos al servidor remoto.
- **git pull**  
  Para bajar los cambios que se encuentran almacenados en el servidor remoto.
- **git clone**  
  Se crea una copia exacta del proyecto que se encuentra almacenado en el servidor remoto.


### CONFIGURACION
Con esto lo que hacemos es colocar el nombre y el correo. (Esto lo pide git para los logs):
~~~
juliorhode@Osiris:~/Escritorio/Git$ git config --global user.name "JulioRhode"
juliorhode@Osiris:~/Escritorio/Git$ git config --global user.email "juliorode@gmail.com"
~~~
### GIT INIT
Para indicar a nuestro proyecto que vamos a utilizar git, realizamos lo siguiente:  
~~~
juliorhode@Osiris:~/Escritorio/Git$ git init
Inicializado repositorio Git vacío en /home/juliorhode/Escritorio/Git/.git/
~~~
### GIT STATUS 
Aqui podemos observar todos los archivos que estan pendientes:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status                            
En la rama master

No hay commits todavía

Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)
        Git.txt
        app.js
        index.html

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
~~~

### GIT ADD 
Con esto agegamos uno por uno los archivos que esten en espera:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git add app.js 
juliorhode@Osiris:~/Escritorio/Git$ git add index.html 
~~~
### GIT ADD .
Con esto agregamos todo lo que esta en espera:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git add .
~~~
Vamos a ver el status de los archivos agregados:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status
En la rama master

No hay commits todavía

Cambios a ser confirmados:
  (usa "git rm --cached <archivo>..." para sacar del área de stage)
        nuevo archivo:  app.js
        nuevo archivo:  index.html
~~~
### GIT COMMIT -M "MENSAJE"
Con este comando, vamos a pasar de la zona de trabajo a pasar el cambio a definitivo, agregando el mensaje que queramos para saber lo que se realizo:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git commit -m "Primer commit"
[master (commit-raíz) 46a79de] Primer commit
 4 files changed, 67 insertions(+)
 create mode 100644 Git.txt
 create mode 100644 app.js
 create mode 100644 index.html
 create mode 100644 style.css
~~~
### GIT LOG 
Aqui podemos verificar todos los commits que hemos realizado:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git log
commit 46a79de9c4470e290ce81aa8a7c724dc2f7543db (HEAD -> master)
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 14:55:39 2020 -0400

    Primer commit
~~~

### GIT CHECKOUT -- nombre_archivo
Para volver al cambio anterior
~~~
juliorhode@Osiris:~/Escritorio/Git$ git checkout -- index.html
~~~
### GIT DIFF nombre_archivo
Con esto vemos la diferencia entre los cambios commiteados y los que estamos realizando. 
**(- lo que he quitado) (+ lo que he agregado)**:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git diff index.html
diff --git a/index.html b/index.html
index 81c544c..94e3501 100644
--- a/index.html
+++ b/index.html
@@ -2,7 +2,7 @@
 <html lang="en">
 <head>
     <meta charset="UTF-8">
-    <title>Document</title>
+    <title>Primera Pagina</title>
 </head>
 <body>
~~~
Primeramente, vemos que hubo un cambio en el archivo index.html.  
Aparte, se puede apreciar en la salida del codigo anterior, vemos que el index.html tenia como titulo **Document**, mostrandolo `- <title>Document</title>`  y ahora luego del cambio, contiene como titulo **Primera Pagina** indicando de esta forma `+ <title>Primera Pagina</title>`.

Vamos a realizar el commit:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git commit -m "Se agrego un titulo en el index.html" 
[master 9de5c69] Se agrego un titulo en el index.html
 1 file changed, 1 insertion(+), 1 deletion(-)
~~~
Ahora veamos los cambios que se han realizado en el archivo index.html
~~~
juliorhode@Osiris:~/Escritorio/Git$ git log
commit 9de5c69a5e51ebccb07b40266c03356b87e13c5c (HEAD -> master)
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 15:07:08 2020 -0400

    Se agrego un titulo en el index.html

commit 46a79de9c4470e290ce81aa8a7c724dc2f7543db
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 14:55:39 2020 -0400

    Primer commit
~~~
### PARA IGNORAR ALGUNA CARPETA O ARCHIVO
Puede darse el caso que tengamos archivos o carpetas que no queremos subir al repositorio porque realmente no nos interesa.  
Vamos a agregamos una carpeta test con un archivo index.js.  
  
Como veremos a continuacion nos indica que tenemos una carpeta test/
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status                  
En la rama master
Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)
        test/

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
~~~
### .GITIGNORE
En este archivo colocaremos todo lo que queremos ignorar. Asi que crearemos un archivo **.gitignore** en nuestro proyecto y **ESTE SI DEBEMOS ALMACENARLO**  
  
Dentro del archivo .gitignore vamos a colocar **test** para nuestro caso de ejemplo.

**NOTA: TODO LO QUE ESTE DENTRO DE LA CARPETA test, SERA IGNORADO**  
  
Luego que lo guardemos, esto es lo que sucede:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status
En la rama master
Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)
        .gitignore

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
~~~
Vamos a agregar el archivo .gitignore:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git add .gitignore 
~~~
Verifiquemos ahora el status:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status
En la rama master
Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
        nuevo archivo:  .gitignore
~~~
Vamos a crear un archivo que queramos ignorar. Lo llamaremos **ignorar.txt**.
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status
En la rama master
Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
        nuevo archivo:  .gitignore

Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)
        ignorar.txt
~~~
Realizamos lo mismo en el archivo .gitignore y colocamos el nombre de **ignorar.txt** debajo del anterior que habiamos colocado.
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status
En la rama master
Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
        nuevo archivo:  .gitignore

Cambios no rastreados para el commit:
  (usa "git add <archivo>..." para actualizar lo que será confirmado)
  (usa "git restore <archivo>..." para descartar los cambios en el directorio de trabajo)
        modificado:     .gitignore
~~~
Ya como agregamos los cambios, vamos a realizar commit:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git commit -m "He agragado un gitignore"
[master 6fb9bfa] He agragado un gitignore
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
~~~
### GIT BRANCH 
Los branchs son como una especie de foto que se toma de tu proyecto, para luego hacer alteraciones. Los branch son ramificaciones de tu codigo.  
  
Si queremos ver las ramas:
~~~
 juliorhode@Osiris:~/Escritorio/Git$ git branch 
* master
~~~
Para crear una rama nueva:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git branch login
~~~
Ya que creamos la nueva rama, vamos a verla:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git branch 
  login
* master
~~~
Para seleccionar la rama que queramos utilizar (en este ejemplo sera **login**):
~~~
juliorhode@Osiris:~/Escritorio/Git$ git checkout login 
M       .gitignore
Cambiado a rama 'login'
~~~
Ahora nos indica la salida, que estamos usando la rama login: 
~~~
juliorhode@Osiris:~/Escritorio/Git$ git branch 
* login
  master
~~~
Ahora como estamos en una rama alterna, ya podemos ir creando archivos y/o carpetas.  
Vamos a crear una carpeta en nuestro proyecto llamada **autenticacion** y dentro un archivo llamado **index.js**.   
  
Si verificamos el status, veremos lo siguiente:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status 
En la rama login
Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)
        autenticacion/
        index.js
~~~
Vamos a agregar todos los archivos que estan en espera (Esta oportunidad no lo haremos uno a uno):
~~~
juliorhode@Osiris:~/Escritorio/Git$ git add .
~~~
Verifiquemos:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status 
En la rama login
Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
        nuevo archivo:  autenticacion/index.js
        nuevo archivo:  index.js
~~~
Vamos a realizar el commit:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git commit -m "Version alternativa con un login"
[login c598023] Version alternativa con un login
 3 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 autenticacion/index.js
 create mode 100644 index.js
~~~
Vamos a revisar el log a ver que es lo que ha pasado:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git log 
commit c5980231acc4a3b7079c15abbe5016422772e0ba (HEAD -> login)
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 15:44:58 2020 -0400

    Version alternativa con un login

commit 6fb9bfa7ff8b7edb4ba07c076effd069174e776a (master)
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 15:28:19 2020 -0400

    He agragado un gitignore

commit 9de5c69a5e51ebccb07b40266c03356b87e13c5c
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 15:07:08 2020 -0400

    Se agrego un titulo en el index.html

commit 46a79de9c4470e290ce81aa8a7c724dc2f7543db
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 14:55:39 2020 -0400

    Primer commit
~~~
Vamos a revisar las ramas para cambiarnos luego:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git branch 
* login
  master
~~~
Vamos a cambiarnos a la rama **master**:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git checkout master 
Cambiado a rama 'master'
~~~
Cuando lo hagamos, vamos a observar que **los archivos que habiamos creado en la rama login, se han desaparecido de nuestro entorno de desarrollo.** Y si vemos los cambios, solo vamos a ver los commit que pertenecen a la rama que nos encontramos.  
Esto se debe a que los otros cambios que habiamos realizado, se encuentran en la rama **login**.
~~~
commit 6fb9bfa7ff8b7edb4ba07c076effd069174e776a (HEAD -> master)
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 15:28:19 2020 -0400

    He agragado un gitignore

commit 9de5c69a5e51ebccb07b40266c03356b87e13c5c
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 15:07:08 2020 -0400

    Se agrego un titulo en el index.html

commit 46a79de9c4470e290ce81aa8a7c724dc2f7543db
Author: JulioRhode <juliorode@gmail.com>
Date:   Mon Feb 24 14:55:39 2020 -0400

    Primer commit
~~~
### AGREGAR REPOSITORIO REMOTO 
Esto nos sirve para almacenar nuestro codigo del proyecto que se encuentra de forma local, a un servidor (en nuestro caso GitHub).  
Cabe destacar, que ya creamos el respositorio en GitHub y copiamos la ruta que nos suministra para la clonacion del mismo:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git remote add origin https://github.com/juliorhode/Git-Fazt.git
~~~
Si verificamos, aparentemente no ha pasado nada, pero ya esta agregado el servidor remoto:
~~~
juliorhode@Osiris:~/Escritorio/Git$ git status 
En la rama master
nada para hacer commit, el árbol de trabajo está limpio
~~~
Ahora, vamos a subir nuestros archivos a la rama master del repositorio remoto: 
~~~
juliorhode@Osiris:~/Escritorio/Git$ git push -u origin master
Username for 'https://github.com': juliorhode
Password for 'https://juliorhode@github.com': 
Enumerando objetos: 15, listo.
Contando objetos: 100% (15/15), listo.
Compresión delta usando hasta 2 hilos
Comprimiendo objetos: 100% (11/11), listo.
Escribiendo objetos: 100% (15/15), 1.81 KiB | 123.00 KiB/s, listo.
Total 15 (delta 4), reusado 0 (delta 0)
remote: Resolving deltas: 100% (4/4), done.
To https://github.com/juliorhode/Git-Fazt.git
 * [new branch]      master -> master
Rama 'master' configurada para hacer seguimiento a la rama remota 'master' de 'origin'.
~~~
Recuerda, que los archivos de la rama **login** no se subieron, asi que vamos a subir los archivos que pertenecen a la rama login: 
~~~
juliorhode@Osiris:~/Escritorio/Git$ git push -u origin login
Username for 'https://github.com': juliorhode
Password for 'https://juliorhode@github.com': 
Enumerando objetos: 6, listo.
Contando objetos: 100% (6/6), listo.
Compresión delta usando hasta 2 hilos
Comprimiendo objetos: 100% (2/2), listo.
Escribiendo objetos: 100% (4/4), 499 bytes | 499.00 KiB/s, listo.
Total 4 (delta 0), reusado 0 (delta 0)
remote: 
remote: Create a pull request for 'login' on GitHub by visiting:
remote:      https://github.com/juliorhode/Git-Fazt/pull/new/login
remote: 
To https://github.com/juliorhode/Git-Fazt.git
 * [new branch]      login -> login
Rama 'login' configurada para hacer seguimiento a la rama remota 'login' de 'origin'.
~~~
### CLONAR REPOSITORIO 
Si por alguna razon, nuestro proyecto local se daño, se borro, etc... podemos clonar el repositorio que se encuentra en el servidor remoto y recuperar todo nuestro poryecto.
~~~
juliorhode@Osiris:~/Escritorio/Git$ git clone https://github.com/juliorhode/Git-Fazt.git

juliorhode@Osiris:~/Escritorio/Git$ git clone https://github.com/juliorhode/Git-Fazt.gitClonando en 'Git-Fazt'...
remote: Enumerating objects: 18, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 18 (delta 5), reused 14 (delta 4), pack-reused 0
Desempaquetando objetos: 100% (18/18), 2.44 KiB | 357.00 KiB/s, listo.
~~~
