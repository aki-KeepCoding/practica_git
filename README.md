# Ejercicio Git

- **¿Qué comando utilizaste en el paso 11? ¿Por qué?**

```sh
$> git reset --hard HEAD~1`
```

El comando `git reset --hard HEAD~1` se lleva el *"puntero"* HEAD al commit padre junto con la rama actual (en nuestro caso *styled*). El modificador `--hard` descarta cualquier cambio pue pudiéramos tener en el Working Copy.

- **¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?**

```sh
$> git reflog
eb87e3b HEAD@{0}: reset: moving to HEAD~1
**4c7fb56** HEAD@{1}: commit: Estilizamos el git-nuestro.mdwq
eb87e3b HEAD@{2}: checkout: moving from master to styled
eb87e3b HEAD@{3}: commit: Creamos el fichero git-nuestro.md
be14482 HEAD@{4}: clone: from https://github.com/akixe/kc-ejercicio_git.git

$> git reset --hard 4c7fb56
```


Primero obtuve el hash del commit al que pertenecía el objetivo con `git reflog`. 

El modificador `--hard` es necesario para descartar el el estado actual de *git-nuestro.md* (sin estilización)

- **El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?**

Seguimos en la rama styled

```sh
$> git merge master
Already up to date
```


No causa ningún conflicto. La rama **styled** ya contiene todos los cambios (commits) de master al ser hijo de éste. Por lo tanto me dice "Already up to date"

- **El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?** 

Sí, causa conflictos. Porque en las dos versiones del fichero *git-nuestro.md* hemos modificado las mísmas líneas.

- **El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?** 

No causa ningún conflicto. Porque **styled** contiene los commits de **master** y por tanto git sólo tiene que llevar la rama **master** hasta el commit al que apunta **styled** (ahora los dos apuntan al mismo commit). Este tipo de merge es de tipo **fast forward** y no crea un commit nuevo para el merge.

- **¿Qué comando o comandos utilizaste en el paso 25?**

```sh
$> git log --graph 
```
Podríamos mejorar el diagrama con `--decorate` (indica ramas) y `--oneline` (una linea para cada commit)

- **El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?**

El commit al que apunta **title** contiene el commit al que apunta **master**, por lo tanto sí podría haber sido de tipo **fast forward**.

Indicando `--no-ff` obligamos a git a crear un commit nuevo que contiene los punteros a los commits de **master** y **title**, moviendo la rama **master** al nuevo commit que hemos generado en el merge no fast forward (**title** se queda apuntando a su commit.) 

- **¿Qué comando o comandos utilizaste en el paso 27?**

```sh
$> git reset HEAD~1
```
- **¿Qué comando o comandos utilizaste en el paso 28?**

```sh
$> git reset --hard
```

- **¿Qué comando o comandos utilizaste en el paso 29? **

```sh
$> git branch -D title
```
Al tener un commit que no se ha *"mergeado"* con ningún otra rama es necesario *"forzar"* el borrado con la opción `-D` (es decir, no es suficiente con `-d`)

- **¿Qué comando o comandos utilizaste en el paso 30?**

He optado por volver al commit que hemos generado en el paso anterior en vez de crear un merge totalmente nuevo:

```sh
$> git reflog (y localizo el merge entre title y master. 

783bc31 HEAD@{0}: reset: moving to HEAD~1
**0adf320** HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
783bc31 HEAD@{2}: checkout: moving from title to master
f077ee4 HEAD@{3}: commit: Añadimos un título a git-nuestro
...

$> git reset --hard 0adf320
```

Si se trataba de rehacer el merge de forma completa, necesitaríamos crear de nuevo la rama title porque para realizar el merge necesitaría esta rama (ahora la tenemos borrada). Para ello:

```sh
$> git reflog 
#(obtenemos el hash del commit correspondiente al que hera la rama title)
$> git checkout [hash rama title]
$> git branch title 
#(creamos de nuevo title)
$> git checkout master
$> git merge --no-ff title
```


- **¿Qué comando o comandos usaste en el paso 32?**

*(Entiendo que tenía que moverme con la rama Master y HEAD a la vez, no sólo con HEAD...)*

```sh
$> git log
#(anoto el hash del primer commit de todos)
$> git reset --hard be1448230e9d034630d39a64413d3155f889267f
```


- **¿Qué comando o comandos usaste en el punto 33?**

```sh
$> git reflog 
#(localizo el merge entre title y master y anoto el hash)
$> git reset --hard 0adf320
```
