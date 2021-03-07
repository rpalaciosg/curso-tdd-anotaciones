# 1. Flujos y organización del trabajo con Git y GitHub

[Material](https://jj.github.io/curso-tdd/temas/git.html)
[Presentación](https://jj.github.io/curso-tdd/preso/git)
[text](https://www.youtube.com/watch?v=Kfzesb-wC5g&t=593s)

## Git y GitHub/GitLab

Debemos configurar nuestra cuenta y configurar en git nuestro email y usuario de git.
No se va a explicar git a detalle. Solo va a dart unos cuantos puntos que vamos a necesitar para trabajar en desarrollo agil.

## Clave publica/privada

Generar una par clave publica/privada para no estar escribiendo mi usuario y contrasenia, trabajar con http esta bien igual.

## Conceptos básicos: pull, pull request, push, clone.

### Pull

Estas mezclando 2 ramas, tu rama principal con una rama remota.
Hay varios tipos de pull:

#### Squash

Se usa cuando estoy trabajando en una rama donde se han hecho muchos commits y no quiero que en la rama principal aparezcan todos esos commits, sino un solo commit firmado por todas las personas que hayan participado.

### Merge commit

Sirven cuando hay una persona encargada de decidir que es lo que entra en la rama principal y entonces se crea un merge osea un commit especifico el cual esa persona firma todos los commits que se van añadir. Toma varios commits y esos commits estas firmados en un solo commit por la persona que ha mergeado.

### Rebase y merge

Funciona como un cierre/cremallera es decir hace un merge metiendo todos estos commits uno encima de otro dejando los commits originales con su autor original y voy a mezclarlos con los commit que tenga localmente con su autor original.

> PAra el instructor es la mejor forma de trabajar

**Ventajas**

- Se conserva la integridad de todos los commits que habido.
- Se conserva la historia y no se hace reescritura de historia osea `squash`
- no firmas cosas que no sean tuyas

## Resolviedo conflictos

cuando trabajo en un `Pull Request` o tratando de fucionar suceden conflictos, esto pasa cuando 2 personas en 2 ramas han hecho una modificación de la misma linea de un mismo fichero.

La forma mas simple de resolverlo es esta:

```shell
git checkout --theirs fichero -> quiere decir que el remoto es el bueno
git checkout --ours fichero -> quiere decir que se conservara mi fichero
```

Aveces suele funcionar a veces no porque son con ficheros que se han borrado, etc.

**Si todo falla** que debo hacer?
Normalmente trabajamos con un repositorio remoto, este puede estar en github, y también tengo el repositorio local, entonces si ya no puedo ir ni para adelante ni para atras entonces voy a guardar mis cambios, es decir copio los ficheros que he modificado y los guardo en otro lugar el que sea.

Luego hago un clone del repositorio original:
`git clone url`

Voy a borrar el _origin_ o el origen definido, asi me lo haya vuelto a clonar:
`git remote rm origin`

Ahora lo que voy hacer es que voy añadir como origen mi fork del original.
`git remote add origin mi-fork-de-url`

Y como se ha hecho un problema y todo falla, y no puedo modificarla de ninguna forma entonces hago
`git push --force`
Y borro lo que hay en mi fork, pongo lo que hay en el fork original, entonces los ficheros que he guardado los copio a mi repositorio les hago commit y ya puedo hacer un pull request.

## Pull Request

> Es una gran ocasión para revisar el código.

Vamos a trabajar con pull request en 2 niveles:

1. Cada vez que saquemos un release de nuestro proyecto lo enviaremos mediante un PR al repositorio del curso, el profesor va a comprobar que se han pasado una serie de requisitos que son los criterios de aceptacion de cada una de las sesiones.

El profesor quiere que aprendas a trabajar con PR y código de otras personas. Leer codigo legacy.

siempre que se vaya agregar algo nuevo en la rama principal hacerlo siempre con PR y siempre que otra persona haya revisado y aceptado los cambios.

Un PR obliga a revisar el codigo, para hacer cambios que esten bien especificados y relativamente atomicos.

## Releasing y tagging

Vamos a trabajar el curso con tags, es decir cada sesion va a tener un release y cada release lo vamos a taggear, entonces es esencial hacer esto en desarrollo agil cada tag lo que va a tener es un producto minimamente viable (MVP) y lo vamos hacer de forma frecuente.

En desarrollo agil se habla de que se tienen un MVP cada dos meses, pero por el curso nosotros lo vamos hacer cada 2 dias.

Para agregar un tag

```shell
git tag -a v0.0.11 -m "First release"
```

el -a nos ayuda a usar Versionado semantico

- major version: es relacionada al numero de sesion del dia. es el primer numero despues de 'v'
  -El segundo numero puede corresponder a diferentes cambios a diferentes PR que hayas hecho
  -El tercer numero equivale a cambios menores, como cambios en documentación, cambios pequenios de reformateo, etc

con -m le damos el nommbre que queramos darle a ese tag o release.

Luego esto despues desde github puedes generar un pdf, agregar un tar.gz o un .zip, incluso si usamos las lineas de ordenes de github.

## Yendonos por las ramas

Lo bueno de las ramas es que luego podemos trabajar con ellas, la idea de los tags es que se les suele llamar como `liteweigth-branch` o `ramas-ligeras`. En realidad un tag no es nada mas que una anotacion o etiqueta que se hace sobre un commit determinado, es como un alias que se le aniade a un commit.

> Recordar que después de asignar un tag debemos hacer `git push --tags`, porque los tags estan en otro indice diferente que los commits comun y corrientes

Si yo tengo un release, lo que puedo hacer es que puedo trabajar con ese release, y si por cualquier razon dices tengo este codigo con este tag en producción y tengo que modificar algo o corregir algo, sin que deje de ser el mismo tag. Entonces puedo descargar ese tag con checkout, tener en cuenta que no son realmente una rama, lo que hace es que te baja al commit donde esta ese tag:

`git checkout v0.0.1`

A continuación debes crear una rama desde ese tag y ya puedes modificar lo que sea

`git checkout -b rama-desde-tag`

Luego fusionarlo, asignarle de nuevo la etiqueta y/o bien fusionarlo con la rama principal, como se quiera.

## Hacer un PullRequest
> Esto lo aprendi despues de haber hecho un Pull sin --rebase

1. Primer creo un fork del repositorio principal en la organización o en mi perfil.
2. Luego clonamos ese fork con `git clone url-repositorio-fork`
3. Luego agrego el upstream del repo principal a nuestro repo fork para tenerlo al dia haciendo lo siguiente con --rebase
  `git remote add upstream url-repo-principal`
  Si queremos verlo podemos escribir `git remote -v`
4. Para bajar los cambios y tener nuestro fork al dia hacemos
`git pull --rebase`