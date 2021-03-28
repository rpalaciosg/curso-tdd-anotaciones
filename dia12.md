# Llevando a cabo los test unitarios

[Video](https://www.youtube.com/watch?v=KgG8SKgu0pM)
[Presentacion](https://jj.github.io/curso-tdd/preso/tests-unitarios.html)
[Material](https://jj.github.io/curso-tdd/temas/tests-unitarios-organizaci%C3%B3n)

# TODO
[x] milestones planteados como productos minimamente viables
[x] Se han integrado tareas en el gestor, como correr el linter, pasar tests.

## Recordatorio: Se comprueban **comportamientos**

No se debe probar sobre implementación sino sobre comportamiento. Que queremos que el código haga, cual es la respuesta, el valor que debe aportar al cliente, es lo que hay que probar.
Los compaortamientos son reflejadoss en las historias de usuarios. Y lo unico que hay que probar son los comportamientos que están en las historias de usuarios, no otra cosa relacionada o que interpretemos de la HUs.

## Los test se ejecutan desde frameworks des test
Son programas eternos o internosk que encuentran los programas d e test en los lugares del lenguje determinado y dicen han pasado tantos test o no han pasado tantos test.s

Elegir un framework de test, hay que ver las posibilidades. En muchos casos vamos a escoger varios determinados.

En el caso de golang en el framework es el propio lenguaje [testing](https://golang.org/pkg/testing/)

Pensar siempre en el framework de test.

## Principios F.I.R.S.T

F: significa que los test sean rápidos, para esto hay una serie de técnicas.
T: timely, escribir los test a tiempo, es decir ante del código.

[Red/green/refactor](https://softwarecrafters.io/javascript/tdd-test-driven-development)

## Lo importante son los tests

Hayy un principio clasico
- Arrange -> Fase setup
- Act -> ejecutar alguna cosa
- Assert _>> hacer asercion, colocar todos objetos

Ejemplo con Typesscript con jest que es un etilo sea BDD (Behavior driven devvelopment)
```typescript
import {Issue, State} from '../Project/Issue';
var data: Issue;

beforaAll(()=> {
  data = new Issue("Foo", 1);
});

test("all", ()=>{
  expect(data.show_state()).toBe(State.Open);
  data.close();
  expect(data.show_state()).toBe(State.Closed);
});
```

Ejemplo de test en golang

## Go es su propio marco de test.
Lo que no tiene go son aserciones, tiene errores pero no aserciones.
- Arrange con testMain
- Act -> 
- Asser - no haces nada oslo cimpruebas si hubo algun error

## Como automatizar los test

### Hooks para test locales
Como vamos a trabajar con git, una de las cosas que tengo dentro  de git son los hooks, que son eventos,

** Crear un git hook** para correr los test, es decir cada vez que hagamos un commit se ejecuten todos los tests llamando a nuestro gestor de tareas en este caso  `make`


## Hito 10
- Pensar y elegir un framework de test
- Empezar a usar el Readme.md  como una verdadera descripción de lo que estamos haciendo.
- Agregar `test` al makefile
```makefile
test:
	go test tests/GoNotes_test.go
```
- En `agil.yaml` una clave  testing
```yaml
testing:
  runner: make test
  framework: go
```