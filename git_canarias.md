que puedo hacer:

* feature en frogr => Ya implementada
* Web de análisis de datos en django. 

```python
>>> os.listdir("/home/anarey/Escritorio/videos_CUSL6")
```

### Poner colores en git

[Colorines en Git](http://www.arthurkoziel.com/2008/05/02/git-configuration/)

    $ git config --global color.diff.meta 'blue black bold'

quedan almacenado en `/home/anarey/.gitconfig`

http://git-scm.com/book/en/Customizing-Git-Git-Configuration

Incluir alias en git:
```
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
```

```
 2002  git format-patch HEAD^
 2003  vi 0001-Actualizado-TODO.patch 
 2004  git reflog 
 2006  git diff
 2007  git log
 2008  git checkout master
 2009  git branch -D recuperar 
 2010  git reflog 
 2011  git checkout -b recuperar HEAD@{4}
```
```
 2020  git add planet/templates/postnew.html
 2021  git status 
 2022  vi /home/anarey/.gitconfig 
 2024  git commit --amend 
 2025  git log -p
 2026  git checkout master
```
```
 2028  git log
 2029  git rebase recuperar 
 2030  git status 
 2031  git stash
 2032  git rebase recuperar 
 2033  git log
 2034  ls
 2035  rm 0001-Actualizado-TODO.patch 
 2036  git stash list
 2037  git stash pop
 2038  git stash list
 2039  git log 
 2040  git config 
 2041  git config --global
 2042  git config --get
```

###  Muestra los ultimas acciones realizadas (últimos cambios, commit, etc)

    git reflog 

 
### Información de configuracion que tenemos activa:

    vi /home/anarey/.gitconfig 

## Crea una rama y cambia a ella, a partir del momento que le indiquemos.

    2005  git checkout -b recuperar HEAD@{1}

 
### Convertir a parch el ultimo commit. Podemos usar el parche después para aplicarlo.

    git format-patch HEAD^

### Muestra toda la información correspondiente al último commit. Con las diferencias.

    git log -p

## Añade el fichero/s del area de trabajo al anterior commit (se olvido incluir un archivo)

    git add fichero
    git commit --amend

## Stash

Es una pila donde podemos almacena cambios (área de trabajo) que necesitamos dejar almacenados porque no se pueda por ahora aplicarlos o porque queremos en otro momento volver a ellos.

    git stash list
    git stash pop

Aplicar commit sin tener en cuenta los cambios que estamos haciendo. Aplica los cambios que haya entre la rama actual y la indicada.

    git rebase recuperar



[Aplicación tmux](http://tmux.sourceforge.net/)
-------------

Contribuir en un proyecto (en el caso de que no tengas permisos sobre el proyecto):

* Hacer un fork del proyecto de github a través de la interfaz gráfica. https://help.github.com/articles/using-pull-requests
* En el caso de que hubieras clonado previamente el proyecto, tienes que cambiar la url del repositorio remoto por el que acabas de crear a través del fork: `git remote set-url origin https://github.com/anarey/GDN.git`
* Lo más conveniente es crear una rama para la nueva feature, hacer los cambios correspondientes y commit sobre esa rama, de forma que no se toque la rama master. Así, en caso de haber cambios en la rama master, se actualizan esos cambios, sin tener que verse implicados con el desarrollo que se está realizando. Y más tarde se hace un merge entre ramas.
* Hacer el commit o los commit implicador.
* Subir los cambios correspondientes al repo (al creado a partir del fork del proyecto principal) 

```
$ git push 
$ git push origin <branch>  # Subir sólo la rama indicada 
```

## Añadir un repo remoto a nuestro repo local.

    git remote add upstream git://github.com/aruiz/GDN.git

```
anarey@tuxiba:~/git/djandoapps/GDN$ git remote -v
origin	git@github.com:anarey/GDN.git (fetch)
origin	git@github.com:anarey/GDN.git (push)
upstream	git://github.com/aruiz/GDN.git (fetch)
upstream	git://github.com/aruiz/GDN.git (push)
```

El pullrequest se hace sobre todos los commit de la rama que que estás haciéndolo.

Tener siempre la idea de lo que se va a hacer y ponerle el nombre a la rama.


* Checkout, cambia a la rama que se le indica, por eso, cuando queremos volver a los cambios anteriores (deshacer los cambios) tb es checkout

```
git checkout -- .gitignore
```

### guardar el estado de cambios de una rama

    git stash save "Configuracion de bd"
    git stash list
    git stash save "Configuracion de bd"

Remotes
----------

Por defecto, la rama remota del proyecto, apuntará a `origin/master`. A nosotros nos intererará que apunte a `upstream/master`. Es decir, cuando hagamos un pull (descargarnos los cambios), queremos hacerlo sobre el proyecto original, y no sobre el proyecto fork.

```
anarey@tuxiba:~/git/djandoapps/GDN$ git remote -v
origin	git@github.com:anarey/GDN.git (fetch)
origin	git@github.com:anarey/GDN.git (push)
upstream	git://github.com/aruiz/GDN.git (fetch)
upstream	git://github.com/aruiz/GDN.git (push)
```

```
anarey@tuxiba:~/git/djandoapps/GDN$ git branch -avv
  anabranch               5edbf76 fix api/views.py
* master                  f552751 [origin/master: ahead 1] Merge pull request #1 from anarey/master
  remotes/origin/HEAD     -> origin/master
  remotes/origin/master   5edbf76 fix api/views.py
  remotes/upstream/master f552751 Merge pull request #1 from anarey/master
```

    anarey@tuxiba:~/git/djandoapps/GDN$ git config branch.master.remote upstream 

```
anarey@tuxiba:~/git/djandoapps/GDN$ git branch -avv
  anabranch               5edbf76 fix api/views.py
* master                  f552751 [upstream/master] Merge pull request #1 from anarey/master
  remotes/origin/HEAD     -> origin/master
  remotes/origin/master   5edbf76 fix api/views.py
  remotes/upstream/master f552751 Merge pull request #1 from anarey/master
```
```
anarey@tuxiba:~/git/djandoapps/GDN$ git pull -v
From git://github.com/aruiz/GDN
 = [up to date]      master     -> upstream/master
Already up-to-date.
anarey@tuxiba:~/git/djandoapps/GDN$ git pull upstream master ^C
```

### Un git pull es equivalente a:

```
anarey@tuxiba:~/git/djandoapps/GDN$ git fetch --all
Fetching origin
Fetching upstream
```
```
anarey@tuxiba:~/git/djandoapps/GDN$ git merge upstream/master 
Updating 5edbf76..f552751
Fast-forward
```

### git rebase

Hace un merge ordenado. Caso de que tengamos un cambio en local, y en la rama master haya habido cambios, lo que haría, es aplicar los cambios en nuestro master del remote, y luego aplica sobre el resultado, los cambios que tuvieramos nosotros. 


### origin, upstream son nombres/alias que podemos darle a los repos remoto para referirnos a ellos.

Por defecto, un repo remoto, se le asigna el alias de `origin`, pero podemos asignarle otros nombres.
Con las ramas, siguen un razonamiento parecedo. La rama que se crea por defecto es `master`, es una rama como otra cualquiera, lo unico, que por convención, nos referimos a ella como la rama maestra, la que va a tener el desarrollo principal, como la rama oficial. Después, se crean las ramas en función del trabajo. Y crear una rama por tipo de cambio/featura/conjunto de commit.

Cuando decimos `upstream/master` estamos refiriendonos a la rama master de repositorio remoto con el alias `upstream`.

[Cuando añadimos un repo remoto, por defecto, apunta a origin.]


### Refactorizar

Refactorizas no solo es sacar el coddigo repeido y ponerlo en funciones, sino hacerlo más mantenible. Que permita hacer el codigo mas legible y posibilite su comprensión.

Refactorizar el código, después los test: agrupar funcionalidades, nombres más significativos.

- Test basico, y su «contratest» 

**OJO**:::  hace uso de la función, que devuelve lo que le habíamos dicho nosotros que devolviera, que no es lo que en ese test, en primer momento, va a devolver.

```python
14 def get_site(site):
15     return "www.site.com"
```

```python
42     def test_not_site(self):
43         site = get_site("http://www.site2.com")
44         self.assertNotEqual(site, "www.site.com")
```


### Teclas de vim:

`:new` fichero  
`:vnew` fichero  

`ctrl + w` y flechita  
`may + v` selecciona linea  

`may >` indenta.



### Proceso para definir los casos:

- Caso base / básiso y simple
- Caso negadoa al base.
- Casos concretos.
- Casos extremos/bordes. (que exista o no el parámetro.)
- Casos raros.



### Añadir solo partes del codido de un archivo al commit

    git add -p Fichero

y luego en las opciones elegimos split
y despues seleccionamos cada cambio.

    git log -p => cambios y contenido de los commit.


### Para arreglar una rama

El caso fue que apliqué un commit en la rama que no era. Por lo que, creamos una rama nueva, aplicamos los commit que nos interesan y hacemos un mv sobre ramas y subo los cambios actualizando el repo remoto con los cambios hechos en local.


> Para dejarlo limpio y evitar problemas yo haría:
> `$ git checkout master`  
> `$ git checkout -b temp`  
> `$ git cherry-pick 191772e1794291` # Aplica el commit indicado sobre la rama en la que estamos.  
> `$ git branch -M temp newmethod` # La rama temp toma el nombre de newmethod  
> `$ git push -f origin newmethod` # Actualiamos los cambios del remoto con los añadidos en el local. (-f de forzar)  
>
> Hacía algunos días que no te decía un comando nuevo de git, ¿no? jejeje

Qué he aprendido después del cabezazo:
* Que cuando suba cambios trabajando con ramas, tengo que tener en cuenta la rama en la que aplico el commit :P
* Que si hago un push al repo remoto, está prohibido usar `git commit --amend` :P
* Que las ramas, con `git branch nuevarama` se crean sobre la rama en la que estás :P Por lo que por eso dices al principio de la lista de
comandos que me cambia a la rama master :)

Arreglando el estropicio he practicado:
* Aplicar ciertos commit de otra rama a la rama en la que estamos
* Hacer un «mv» sobre ramas
* «Actualizar» el contenido de una rama remota con el contenido de la rama local que le indiquemos.
* Borrar ramas
* diferencia entre ramas: `git diff --stat master nuevafuncionalidad`
* Listar ramas: `git branch`
* Listar ramas remotas: `git branch -r`


> * Que si hago un push al repo remoto, está prohibido usar `git commit --amend` :P

Bueno, lo puedes hacer, pero si ya has pusheado, no es muy recomendable. Sobre todo si el repo es compartido o hay gente que ya ha hecho fork.

De todas formas, hay dos situaciones en las que yo encuentro útil y no peligroso hacer un `git push -f` tras haber modificado el histórico que ya habías pusheado:
 * Un repo personal que no tienes compartido, que tiene muy pocos commits y que del que nadie ha hecho un fork aún. Por ejemplo, el típico proyecto que subes a guthub y antes de anunciarlo, te das cuenta de un error en los commits (o que te dejaste una password) y lo arreglas antes de publicar el proyecto en twitter.
 * Un pull-request. Si creas una rama para una feature en un proyecto y haces un pull-request, es posible que no lo acepten tal cual.
Después de discutir los cambios en el pull-request, puedes hacer los cambios acordados en la rama, arreglar el histórico y volver a hacer `git push -f` de la rama. Eso actualizará también el pull-request y así se podrá aceptar sin tener que crear uno nuevo con los nuevos cambios.




##########



#### Cadenas:

```python
>>> url = "http://www.anarey.info/acerca-de/mi/en/la"
>>> url_splitted = url.split("://")
>>> url_splitted
['http', 'www.anarey.info/acerca-de/mi/en/la']
>>> path_splitted = url_splitted[1].split("/")
>>> path_splitted
['www.anarey.info', 'acerca-de', 'mi', 'en', 'la']
>>> path_splitted[1:]
['acerca-de', 'mi', 'en', 'la']
>>> path_splitted[:1]
['www.anarey.info']
>>> path_splitted[:2]
['www.anarey.info', 'acerca-de']
>>> path_splitted[1:]
['acerca-de', 'mi', 'en', 'la']
>>> ("/").join(path_splitted[1:])
'acerca-de/mi/en/la'
>>> import os
>>> os.path.join('etc', 'defaults', 'grub.cfg')
'etc/defaults/grub.cfg'
```
