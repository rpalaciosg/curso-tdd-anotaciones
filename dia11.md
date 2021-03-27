# Organizando los tests Unitarios

[Material](https://jj.github.io/curso-tdd/temas/tests-unitarios-organizaci%C3%B3n)
[Video](https://www.youtube.com/watch?v=znWcmIeQc7o)
[Presentacion](https://jj.github.io/curso-tdd/preso/tests-unitarios-organizaci%C3%B3n.html)

## Hito 9:
Elegir biblioteca de `aserciones` en golang  y preparar para los test., ver mejores practicas. 
  - Crear por lo menos los ficheros de test, 
  - decidir como organizar los test como test o subtests
  - Que objetos se van a crear y tambien ir escribiendo la estructura general de las clases que vamos a crear.

Crear en agil.yaml un clave
```yaml
test: 
  - test/fichero-test.jl

aserciones: "@test"
```
Se va a usar [testify](https://github.com/stretchr/testify)