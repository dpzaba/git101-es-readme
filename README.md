# Git 101 en español

1. ¿Qué es Git?
2. ¿Qué son Gitlab y Github?
3. Git en funcionamiento con ejemplos (modo hacker)
4. ¿Pero cómo subo esto a Internet?
5. Gitlab/Github en funcionamiento (modo fácil)
6. Exámen final
7. Quiero algo más fácil


## 1. ¿Qué es Git?

- Sistema de control de versiones para:
  - Controlar cambios de ficheros (de ordenador)
  - Coordinar el trabajo de esos ficheros entre distintas personas

- Creado por Linus Torvalds en 2005 (para desarrollar Linux)

- Según [Stack Overflow](https://insights.stackoverflow.com/survey/2015#tech-sourcecontrol) en 2015 lo utilizaba el 69% de los desarrolladores


## 2. ¿Qué es Gitlab/Github?

- Plataformas para alojar/subir proyectos utilizando Git
- Proyectos pueden:
  - ser públicos (https://github.com/cabify/rubyChallenge) o privados (https://github.com/cabify/product_ruby_core)
  - pertenecer a una organización (https://github.com/cabify/) o individuo (https://github.com/dpzaba)
- Además también ofrecen:
  - Interfaz web para ver el trabajo hecho en Git
  - Merge Requests / Pull Requests
  - Issues
  - Visualizar documentos Markdown, notificaciones, wiki, página web, ver seguidores, estrellas, etc.

## 3. Git en funcionamiento con ejemplos (modo hacker)

### WARNING! hay que empezar a hacer cosas

![](https://media.giphy.com/media/1fMjj5j2Z7chq/giphy.gif)

### Requisitos:

- Linux o MacOS
- Git instalado
- Cuenta en Github o Gitlab
- Abrir una consola/terminal (lo de la pantalla negra con letras blancas)

- Comprobamos la versión de Git

```
git --version
```

- Añadimos un nombre y email en la configuración global de Git

```
git config --global user.name "Mi nombre"
```

```
git config --global user.email "mi-email@example.com"
```

- Creamos la estructura para los ejemplos que vamos a hacer

```
mkdir -p ~/probando-git/3-1-1-ejemplo
mkdir -p ~/probando-git/3-1-2-ejemplo

mkdir -p ~/probando-git/3-2-ejemplo/
cd ~/probando-git/3-2-ejemplo/
git init
echo "Hola, esto es un fichero de texto" > ~/probando-git/3-2-ejemplo/un-fichero.txt
git add ~/probando-git/3-2-ejemplo/un-fichero.txt
git commit -m "Añadido un-fichero.txt"
echo "Hola, esto es otro fichero de texto distinto" > ~/probando-git/3-2-ejemplo/otro-fichero.txt

mkdir -p ~/probando-git/3-3-ejemplo/
cd ~/probando-git/3-3-ejemplo/
git clone ../3-2-ejemplo/ .
git checkout -b estaba-escondida
echo "Ouch! me has pillado!" > ~/probando-git/3-3-ejemplo/fichero-escondido.txt
git add ~/probando-git/3-3-ejemplo/fichero-escondido.txt
git commit -m "No me vas a encontrar"
git checkout master

mkdir -p ~/probando-git/4-1-ejemplo

cd ~/probando-git
git clone https://github.com/dpzaba/git101-es-example-to-fix-collaboratively.git
```


- Las notas que tengan esta forma son sólo para aclarar o explicar detalles:

> Esto es una nota para explicar algo. O un enlace `https://example.com`


- Algunos conceptos que utilizaremos:
  - fichero/archivo
  - commit
  - rama
  - log

### 3.1 ¿Cómo inicio un [repositorio](http://dle.rae.es/?id=W3mzJyE) de Git?

#### 3.1.1. Desde cero

```
cd ~/probando-git/3-1-1-ejemplo
git init
```

> Un repositorio "vacío", pero esto ya es un repositorio de Git (carpeta .git/). Podríamos verlo ejecutando `tree -al`.

#### 3.1.2. Partiendo de algo creado previamente

```
cd ~/probando-git/3-1-2-ejemplo
```


Podemos clonar el repositorio del ejemplo anterior que acabamos de hacer


```
git clone ../3-1-1-ejemplo/
```


> Vaya tontería, ¿no?

Podemos clonar un proyecto publicado en Internet


```
git clone https://github.com/cabify/rubyChallenge.git
```


> La URL la sacamos de `https://github.com/cabify/rubyChallenge`

### 3.2. Ahora algo más interesante

```
cd ~/probando-git/3-2-ejemplo
```

Vamos a ver dónde estamos / en qué estado estamos

```
git status
```


> Vemos la rama y "untracked files"

Añadimos el fichero al repositorio


```
git add otro-fichero.txt
```


Vemos el estado


```
git status
```


> Nos dice que ahora hay "Changes to be committed"

Hacemos commit


```
git commit
```


> Si no nos gusta que se abra un editor de texto, podemos poner el mensaje del commit en la misma linea con `git commit -m "mensaje del commit"`

Una vez tenemos un commit, podemos verlo con


```
git log
```

Vamos a añadir algo más de contenido

> Abrimos el fichero `un-fichero.txt` y añadimos alguna linea más. Si queremos hacerlo por consola es suficiente con `echo "Esto es otra linea" >> un-fichero.txt`

Vemos el estado


```
git status
```

Nos avisa de que hay "Changes not staged for commit", cambios que no se han añadido a Git.

Podemos ver cuales son esos cambios con


```
git diff
```


> Con el símbolo `+` vemos las líneas que son nuevas y con `-` las que se han borrado o modificado.

Lo añadimos, hacemos commit y vamos a ver el log


```
git log
```


> Se puede ver la "historia de Git", los "ids" de los commits, además de la fecha y autor

### 3.3. Ahora con ramas

```
cd ~/probando-git/3-3-ejemplo/
```

Con `git status` veíamos la rama y estado en el que tenemos nuestro repositorio, pero también nos puede interesar saber todas las ramas que tiene nuestro proyecto.


```
git branch
```


> ¿Qué ves?

Podemos movernos de rama con


```
git checkout estaba-escondida
```


> Fijate que ahora tienes un fichero más que en la rama `master` no estaba. Puedes volver a cambiarte a la rama master con el comando anterior para comprobarlo de nuevo. Cuando termines, vuelve a la rama `estaba-escondida`.

No solo podemos tener ficheros "nuevos" en las ramas, también podemos modificar alguno de los que ya teníamos. Elige uno (o varios), modifícalo, añádelo y haz commit.

> Esta vez sin ayuda...

Una vez tengamos nuestra rama con todos los cambios que queramos y hayamos hecho commit, podemos mezclar ambas para que todo se quede en la rama `master`.

Para ello la forma más fácil es irte a la rama donde vas a querer tener la mezcla de ambas.


```
git checkout master
```


Y ahora hacemos "merge"


```
git merge estaba-escondida
```


> Nos muestra un resumen de los cambios en los ficheros al mezclar las dos ramas.

## 4. ¿Pero cómo subo esto a Internet?

```
cd ~/probando-git/4-1-ejemplo
git clone ../3-3-ejemplo/ .
```

Vamos a subir el último ejemplo a un repositorio tuyo en Github

- Ir a tu perfil > repositorios > [Nuevo repositorio](https://github.com/new)

- Añadimos un repositorio remoto

> `git remote add origin https://github.com/XXXXX/YYYYY`

- Subimos nuestra rama

> `git push -u origin master`

Ahora deberíamos poder ver todo en nuestro repositorio en la web

## 5. Gitlab/Github en funcionamiento (modo fácil)

- Página principal
- Perfil personal (repositorios, estrellas, seguidores...)
- Perfil proyecto/empresa/agrupación
- En un repositorio concreto:
  - Commits
  - Ramas
  - Issues
  - Pull/Merge Requests (PR/MR)
  - Estadísticas
  - Visualización de [Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
  - Botón para editar ficheros

- Ejemplo de Cabify:
  - https://gitlab.otters.xyz/
  - https://github.com/cabify/

## 6. Exámen final

![](https://media.giphy.com/media/xT9IggnH2ywRd39XDq/giphy.gif)

[https://github.com/dpzaba/git101-es-example-to-fix-collaboratively](https://github.com/dpzaba/git101-es-example-to-fix-collaboratively)

- `cd ~/probando-git/`
- Crea una rama
- Corrige una errata, añádelo a Git, haz commit y push
- Vete a Github y crea una Pull Request
- Menciona a algún compañero y ponle como revisor
- Visualiza una PR de algún otro compañero, comenta, apruébala o pide que se realicen cambios

## 7. Quiero algo más fácil

- [https://desktop.github.com/](https://desktop.github.com/)

![](https://media.giphy.com/media/yIsbuPCEOgNHO/giphy.gif)


# Referencias

- [Markdown] https://help.github.com/articles/basic-writing-and-formatting-syntax/
- Manual completo de Git en [https://git-scm.com/docs](https://git-scm.com/docs)
