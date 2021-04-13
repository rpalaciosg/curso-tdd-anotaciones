# Tests de cobertura

[Material](https://jj.github.io/curso-tdd/temas/cobertura#Actividad)
[Video](https://www.youtube.com/watch?v=PIlQq-Y4opY&list=PLsYEfmwhBQdJJsCTshZw8Ae67lU48wkaA&index=15)
[Presentación](https://jj.github.io/curso-tdd/preso/cobertura.html)

## TODO
[x] Se ha creado una hoja de ruta en los milestones? Productos minimamente viables de conplejidad creciente.
[x] Se ha configurado un sistema de CI 
[x] Se ha reorganizado la logica de negocio con test de dependencias? Inyección de dependencias si es que se tiene dependencias externas, esas dependencias externas se pasen haciendo inyección de dependencia.

## Si no se ha comprobado, esta roto
Si no se ha hecho un test de algo hay que asumir que eso esta roto o que el código no funciona.

Es difícil saber que no se ha testeado.

Pero por lo general, si se tienen uan metodología de trabajo que primero escribimos los test y luego escribimos el codigo para pasar esos test, es complicado tener código no testeado o comprobado.

Puede suceder que al refactorizar y que por ahi te quede algo sin comprobar. Por eso son imprecindibles los tests de cobertura.

Los test de cobertura no disminuyen la cantidad de defectos en el codigo, pero como todo, crea un ambiente o flujo de trabajo en el que si me acostumbro a tener una cobertura alta, es decir que la mayoria del codigo este testeado, es mas dificil que se introduscan errores, porque tengo una disciplina que ingresarr errores al codigo es mas complicado.

Crea una abmiente o serie de flujo de trabajo si nos acostumbramos a tener una cobertura alta, es dificil tener mas errores.

Como se define la cobertura:

## Cobertura: numero de caminos de codigo que los test ejercitan

No estamos diciendo que la cobertura es el codigo que efectivamente se ejecuta, para eso estan los profiles que tienen algo que ver con los test. 

Es saber que caminos estan cubiertos por test. Todos los posibles camino de codigo, todas las ramas, los bucles estan ejercitados por test.


## Buscar el nivel ideal de cobertura

Cada organizacion yy equipo debe buscar el nivel adecuado de cobertura, esto porque porque tiene algo especial o porque es complicado de testear.

Debes ponerte d3e acuerdo y establecer un nivel de cobertura de 60% que es aceptable, 70% es bueno, y 90% es excelente.

A nivel global, a nivel de modulo, a nivel de función mínimo un 80%

Se pueden usar los test de cobertura para identificar codigo muerto, que es codigo que ha dejado de usarse, y que se puede eliminar. PEro sirve para realmente ver que todo el codigo que se esta usando es realmente util, que se esta ejecutando y que esta dando la salida oc omportamiento deseado.

Es importante para poyectos libres, usarlo para codigo añadido, cuando haces un PR, ese PR puede corregir, refactorizar o add una caracteristica nueva, lo que es importante es que ese codigo nuevo no disminuya el nivel de cobertura que ya tienes en tu codigo, es decir que se quede igual o que suba la cobertura.  si por alguna razón crea nuevos caminos de codigo esos caminos deben estar testeados y cubiertos.

Hay algo bienimportante en los test:

En los test hay edge cases y corner cases:, son casos excepcionales, en el sentido de que estan al borde de los valores posibles de una estructura de datos o de una variables, ejm. Por ejemplo para una cadena cuales serian los edges cases? Ps serian cadena vacia, cadena con 750000 caracteres, cosas por el estilo. Todas esas cosas convienen que se ejerciten.
En muchos caso esto sifnifica qe vas a tener que aniadir test que no esten realmente realcioados con casos posibles que tenga en una historia de usuario. Siempre hay que tener en cuenta esas posibilidades.

## En combinación con el profiler, identificar cuellos de botella
Los cuellos de botella van a ser caminos de codigo que tarden en ejecutarse mas de la cuenta, con mucha frecuencia. Y haran que crwearan una secuencia determinaada y tardaran.
Mirando lo que te dan los test de cobertura y los profilers,
Los proiflers miran los camnios de codigo que se ejecutan cuando tu estan ejecutando tu programa en produccion.

Con estos podemos ver que funciones se estan llamando mas veces, o menos veces y saber a cual tendria que ponerle mas atención.

Mi base de codigo, debe alcanzar un estado de ZEN, de conocer bien que es lo que esta sucediendo. Que etructuras se estan creando o destruyendo, para eso hay un monton de herramientas interesantes.

Profilers con test de cobertura es lo que tenemos que usar todo el tiempo.

## Elegir un marco/servicio de cobertura.

Son 2 cosas diferentes. Marco es lo que ejecuta o crea la instrumentacion suficiente para recoeger todas las llamadas para gener un fichero. Ese fichero se renderiza de una forma determinada, como json, html, con graficos.

Los servicios de covertura, hay servicios gratuitos y de pago, o de pago con un tier gratuito.

Te das de alta te dan un token, que si integramos el token, tenemos que subirlo al sistema de integracion continua y gestionarlo con una variable de entorno.

Cada vez que haga los test de covertura, me lo presentara en el dashboard.

## Generación de informes a partir del codigo

Como usarlo en la practica.
- Primero se deben ejecutar los test
- Despues de ejcutar se dice generame un informe que diga cual es la cobertura de estos test.

En este ejemplo de go que ya tiene todo incluido, con `--coverprofile` le das el fichero de donde guardar la informacion.

```shell
go test -- coverprofile=coverage.out
```

Esos ficheros guardan en un formato especifico de la herramienta, en unos casos son textos, a partir de eso suelen haber herramientas externas que permiten visualizar esos informes.

Si aplicamos Refactorizacion se nos mostrara que esta cubierto.

Los test de cobertura realmente ayudan un monton, cuando estas escribiendo los tests. Ayuda a encontrar errores. Sobre todo si lo agregas al principio y te ahorras en reactorizacion posterior.


## Integrar los tests de cobertura en integracion continua

Hay que tomar el sistema que se este usando y meterlo en los sistemas de integracion continua. Lo que usa para cobertura se usa nyc para typescript, estos se integran bastante bien con jest y funciona bastante bien, ejecuta los test de cobertura y sube el informe a codecoverage.

Como toda tarea que se debe hacer de forma autonatica, integra en el gestor de tarea y segundo en el sistema de integracion continua.

## TODO hito 13

- Configurar los test de cobertura e integrarlos en CI.

Esto como lo va  hacer el gestor de tareas o task runners,  agregar una tarea que sera `coverage` y entonces en la descripcion que tengamos en el README.md tomare el comando del gestor de tarea en el agil.yaml y comprobara que en el README este la frase o la estanza lo que sea coverage ya sea `make coverage`, `npm coverage` o [comando] coverage

- En el Readme meter un Badge de codecov con cobertura aceptable. (Aceptable es lo que decidamos en el squad. encima del 60% es aceptable pero debemos decidirlo nosotros).


Para realizar esta tarea me apoye de los siguientes recursos:
- [Getting started ith code coverage for golang](https://about.codecov.io/blog/getting-started-with-code-coverage-for-golang/)
