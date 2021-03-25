# Organizando la implementacion

[Material](https://jj.github.io/curso-tdd/temas/organizando)
[Presentacion](https://jj.github.io/curso-tdd/preso/organizando.html)
[Video](https://www.youtube.com/watch?v=zKcdn0WExbw&feature=youtu.be)
[Hito](https://jj.github.io/curso-tdd/temas/organizando#actividad)

## Metodologia de los 12 factores.

## Metadatos segun el formato del lenguaje


## Usar gestores de versiones
- Recomienda usar gestorer de versiones para el lenguaje que vayamos a usar. Emj. pyenv en python, nvm en nodejs.

## El codigo debe ser simple | Principio de disenio
Una clase debe ser lo suficientemente grande apra que tu mente lo pueda recordar.

- Responsibilidad unica: SOLID, SHOC

Hay unos principios similares llamados [SHOC](https://codemanship.wordpress.com/2021/03/03/forget-solid-say-hello-to-shoc-principles-for-modular-design/)

- Esconder implementacion, H de "hide", usar variables privadas.

- Inversion de dependencias: SOLID, SHOC, es uun patron, si una clsae estaa acoplada con otra, lo que hace es que inviertes las dependencias de forma que una clase tenga que decir de que otra clase depende y eso se haga en tiempo de ejecucion.

## Los hitos se organizan alrededor de productos minimamente viables
Tenemos que planificar/organizar la programación.
Primero debes tener el disenio, que es un hito, los hitos son ortogonales, perpendiculares a las epicas.

## Los hitos: hoja de ruta del desarrollo
Milestone, se traduce como piedra millar.
Penesar los hitos no como parte del disenio sino como algo a lo que vas a llegar.

## TODO hito 5
- Organizar una hoja de ruta con milestones: es decir primero vamos a crear el disenio de las clases y ese seria el primer hito de nuestro proyecto.
En el hito 2 lo que voy hacer es implementar esta historia de usuario y esta historia de usuario que tiene un nivel de abstraccion mas baja.
La podemos organizar como una ficha en nuestro camban, pero lo importante es escribir y describir, crear los hitos en nuestro proyecto.

Seguir un esquema iterativo que se lo vay haciendo continuamente, empezamos con el disenio de las clases, la  implementacion de historias de usuario en esas clases y asi sucesivamente.