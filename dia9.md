# Gestores de tareas y su importancia en automatización del desarrollo.

[Material](https://jj.github.io/curso-tdd/temas/gestores-tareas)
[Presentacion](https://jj.github.io/curso-tdd/preso/gestores-tareas.html)
[Video](https://www.youtube.com/watch?v=R4kAkiJhspQ)
[Hito](https://jj.github.io/curso-tdd/temas/gestores-tareas#actividad)

Hablar de gestor de tareas a la hora de programar agilmente o de hacer un desarrollo agil es esencial.

Porque todas las tareasa que se hagan dentro de un ambiente de desarrollo y despliegue deben estar configurados de una forma standar y buenas practicas.

## TODO
[x] Se han rehecho las HUs con las personas?
[x] Hemos comenzado a organizar el desarrallo en milestones?
[x] Se han diseniado clases y excepciones, no anto programar sino diseniarlas, saber que atributos y estructuras de datos van a tener esas clases y saber que excepciones van a lanzar esas clases.

## TODO:retro
 [x] Se ha comprobado el formato del fichero YAML? Agregar el github action y agregarlo a nuestro repositorio.
 [x] Yaml siempre termina en retorno de carro, o error de sintaxis.

 ## configuración en el entorno.

En el desarrollo siempre hay una serie de tareas que se debe hacer, desde compilar, pasar los test y desplegar la aplicacion.
Esas tareas que son comunes hay tareas que no son comunes y que queremos automatizar.

La idea de trabajar con desarrollo nativo en la nube con desarrollo agil es que debe estar todo automatizado, y esa configuracion del entorno de como hacer ciertas tareas debe estar programador osea debe estar en el entorno es decir tiene que estar como codigo algun sitio.

Es decir no puedo tener un README que este en cualquier lado. Todo eso debe estar hecho de forma estandar. Al final se ejecutan usando task runners o task managers.

**Unificar y programar tareas**, que podamos usar lenguajes de alto o bajo nivvel para programar esas tareas para que sean repetibles y replicables.

## Task runners, build managers, compiladores y gestores de dependencias

Hay 3 conceptos que tienen un continuo pero que no son lo mismo:

### Gestores de dependencias
Son programas que sirven para describir en un ichero de que bibliotecas depende mi proyecto, decir la version del lenguej de programacion que tenemos y una serie de metadatos. Los ejecutamos instalan las dependencias, hay muchos tipos.

### Compiladores
HAcen cosas adicionales, soncompiladores que aveces ejecutan test, instalan dependencias o generar ficheros de configuracion, sobre todo en lenguajes modernos.

### Build managers

Los gestores de compilacion, lo que hacen es esencialmente es lenguajes compilados o que tengan una fase en la cual se genera un  fichero objeto o transpilado, lo que dicen es estas son las reglas que hay para construir los ficheros que esencialmente van a servir para desplegarse a partir de los ficheros fuentes.

Lo que quiero ahora es generar la documentación.

## Task runners

Son o pueden ser build managers, o compiladores y en algunos casos pueden gestionar dependencias, pero esencialmente lo que hace es que yo quiero ejecutar estas tareas, en otros casos mas avanzados hacen un grafo que dicen que tareas se deben lanzar de acuerdo a un fichero.
*ejecutan tareas*
Gestor de dependencias que ejecutan tareas ejemplo es **npm**
Casi siempre vamos a necesitar y es esencial tener un task runners., por que desde ahi va a lzar tareas necesarias desde los sistemas de integracion continua y demas.

Lo que el instructor quiere es que siempre se ejecuten los test desde un task runners.
Y lo que necesitemos para ejecutar un test lo tenga conigurado en un task runners.

## diferencias en configuración, standarizacion, forma (imperativa o declarativa), especificidad

Hay una  gama completa de task runners.
- diferencias en configuracion: algunos necesitan esepcificamente que hacer otros lo hacen automaticamente.
- estandarizacion: siguen un proceso estandar
- formas: 
  - imperativa:cuando sucede esta tarea quiero hagas esto
  - declarativa: es mejor e interesante, porque dice yo lo que quiero es que el sistema quede en ese estado, y puedo describir reglas para alcanzar ese estado a mi lo que m interesa el estado final: EJm. `makefile` es declarativo, make es una obra de arte y es mucho mas potente de lo que hay y lo mejor para la vida moderna, y tiene un lenguaje my atemorizante. 
- Hay task runners que son especificos y otros genericos ejm make,se usa para programas con c, javascript, golang. La eleccion de un task runners no es tan obvia hay un error al elegir npm al usar javascript pero hay make, hay gulp, grunt. Siempre debes tomar deciciones tecnicas y buscar cuales son las mejores practicas del area.

## Muchos incluyen DSL
domain specific languaje como make. son lenguajes que son especificos de dominio que tienen reglas especificas. el DSL de make esta enfocado a crear reglas.

## Las tareas tienen nombres estandar
Si hago una tarea que todo mundo hace debo hacer que se llamen iguales, si voy hacer test, la tarea se debe llamar `test` no `tests`.
- install: sirve para instalar la aplicacion no las dependencias de la aplicacion
- instal-deps: instalar dependencias de la aplicacion
- build: para compilar y genewrar los ficheros.
- test
- check: fichero de comprobacion com lint, comprobacion autografica
- docs: generar documentacion

En estas cosas no hay que innovar sino usar lo que ya hay.

## Ejemplo gestor de tarea Maskfile: tareas en markdown

Lo que hace es que describes las tareas en un archivo markdown, el titulo del fichero markdown sera el titulo de la tarea.

Encabezzamiento de segundo nivel es el nombre de la tarea, en este caso podman-images

```Maskfile
# Tareas para este proyecto

## podman-images

> Crea imagenes de Docker a partir del Dockerile usando Podman

~~~sh
podman build -f nodata.Dockerfile -t jjmerelo/hitos/data
podman build -f dockerfile -t jjmerelo/hitos/hugitos
~~~
```

El comando se llama `mask` y si hago `mask help` me va a decir las tareas que tiene. al igual que si hago make help.

Tiene algo que son las delimitaciones de codigo markdown las usa para saber el interprete que se va a usar para ejecutar esa tarea. Al instructor le gusta mas que `make` porque todo lo tenemos en un fichero markdown simplemente lo edito, en make puedo ejecutar tareas pero lo tengo que ejecutar desde el shell. 
yo puedo ejecutar tareas shell, o tareas perl, o tareas python con maskfiles, esta escrito en rust, solo lo instalo lo pongo en el path y ya podemos construir cosas, es generico e imperativo, y lo puedo usar para cualquier lenguaje.

## Clasico Makefile
Lo puedo usar con cualquier lenguaje de programacion. Tenemos que ir directo con el manual de referencia.

```makefile
%:
  go $@
```
Lo que paso en %: lo reemplaza en $@

Si escribo make test. Puedo poner uchas reglas posibles en el orden de prioridades.

## Ake en Raku
Esta escrito en Raku

## Poetry en Python: gestor de dependencias
Es el resultado de los utlimos PEPS, es una herramienta que usa un formato que se parecen a los ficheros `.ini` pero en realidad es n archivo `.toml`.
Tiene como apartados standars.

Aqui lo interesante y aqui es donde poetry sirve como gestor de tareas, solo si son tareas que estan escritas en python.

## Un gestor de dependecias rara vez es suficientes


## Actividad: hito 7
- Elegir un gestor de tareas.
- yo piendo que maskfile llama mas la atencion y permite escribir cosas en cualquier lenguaje que este instalado en el sistemas.
- Se comprobara el fichero de taras/lenguaje. En algunos casos ciertos lenguaje tiene getores de tareas recomendados. entonces debemos agregarlo al archivo `agil.yaml` lo siguiente:
```yaml
lenguaje: "Golang",
taskile: "Makefile" o "Maskfile"
```

