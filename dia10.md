# Hacia los tests unitarios - hito 8

[Video](https://www.youtube.com/watch?v=JKXykxpG_0o)
[Presentacion](https://jj.github.io/curso-tdd/preso/hacia-tests-unitarios.html)
[Material](https://jj.github.io/curso-tdd/temas/hacia-tests-unitarios)

## TODO
[x] Milesstones
[x] Se han diseniado excepciones
[x] Se ha elegido un task runner y empezar a configurarlo.

## TODO retro
- Cerrar los issues desde un commit (o PR)? Si sigue dando error porque no lo cerraste en el commit, mejor borrarlos.

## El mejor codigo es el que no se escribe

Organizar nuestro codigo de forma que tengamos que escribir el minimo codigo posible, ahorra tiempo, codigo y errores.
En vez de escribir comprobaciones o assersiones, hay que escribir el codigo de forma que no se pueda cometer ciertos errores.

### Codigo declarativo FTW
El codigo dice debe ser de esta forma, como se declaran estas clases.

## DRY: No te repitas
Es un principio importante, porque cuando encuentras codigo que se repite revel un problema ssudyacente. 
Que ocurre cuando tienes que refactorizar el codigo? cambias una de las instancias o varias.

**Limpia tu codigo** no debes tener o enceontra codigo repetido

En nuestro caso de nuestra solucion, debemos crear solo una clase materia que tenga todo, esto para evitar repetir.

DRY es un olor de codigo.

Hay un antipatron que dice cuando.
Siempre que encuentres repeticion piensa pporque estas repitiendo, y ver si hay que sacarr una funcion a parte.

## Evitar los numeros magicos
Otra cosa que evita posibles errores. Son cadenas magicas o literales que se usan como argumentos de funciones o argumentos para instanciar una clase, el codigo limpio no debe tener encatanmiento.

**Codigo limpio sin encantamientos**


## Algo huele mal en tu codigo
No escribir pensando solo en los test. 
A pesar de que compile y funcione, no siempre p.puede ser correcto.
- Code smells, codigo idiomatico (codigo para que solo el compilador lo entienda), antipatrones y otros pecados.

son cosas que se pueden identificar con un analisis estático de codigo.

## Usa linters
Significa pelusilla en espanol.
Lo que pretenden es eliminar esa pelusilla que hay en el codigo.
Examinan estaticamente el codigo, dan consejos para respetar convenciones.
Suelen ser configurables y plugables y permiten usar o no recomendaciones.

Usarlos al momomento que empiezas a escribir codigo, evitara refactorizxar codigo entero.
Encontrara cosas que no son errores tipograficos.

El linter te dice si tu codigo apesta o no.

La documentación de codigo no esta en contra de clean code, clean code esta en contra de los comentarios.
Nos ayuda a seguir la convención al momento de escribir codigo.

Tengo que buscar linters para golang. Tengo que pasarlo a mano 


## Hito 8
En este hito debemos elegir un linter, integrarlo a nuestro proyecto y empezar a usarlo, asi sea que lo ejecutemos de forma manual.

En el `agil.yaml` debemos agregar el nombre del linter a usar para nuestro proyecto.

```yaml
linter: linter-que-usemos
```
Agregar al fichero de tareas `makefile` la tarea **check* y lo que ejecute esa tarea sea el linter.

PAra eso estamos usando [vet](https://golang.org/pkg/cmd/vet/)
PAra correr o ver los _checks_ sisponibles escribir `go tool vet help`
debemos agregar estos checks en el macke file con una tarea `check` que los ejecute.

Recomendado instalar linter de Sonar lint de SonarCube en Visual Studio Code.
Tambien hay linter commo golint
Podemos ver aqui los linters en golang.
https://medium.com/wesionary-team/introduction-to-linters-in-go-and-know-about-golangci-lint-6486fb2864b3


 