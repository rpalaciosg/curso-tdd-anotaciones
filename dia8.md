# Comenzando a programar
> Practicas defensivas de programación

[Material](https://jj.github.io/curso-tdd/temas/a-programar)
[Presentacion](https://jj.github.io/curso-tdd/preso/a-programar.html)
[Video](https://www.youtube.com/watch?v=nSuo-03IW-k)
[Hito](https://jj.github.io/curso-tdd/temas/a-programar#actividad)

## TODO
[x] Se han usado losgs y otros servicios
[x] Se han rehecho las HUs con las personas, en el archivo agil.yml
[x] Hemos comnezado a organizar el desarrollo en milestones?
  Siempore se cierra un issue desde el commit 

## TODO retro
- Usando `pull --rebase` 
- O hacer un fork sobre la marcha es decir desde la web de github.
- Se ha comprobado el formato del fichero yaml? Lo mejor es que crees un programa que te lo genere, o usar un linter de yaml.

## Programar para tu yo del futuro
Siempre programar para tu yo del futuro o la siguiente persona que vaya  ver tu código.
Tienes que programar para tu yo del futuro.
- abraza erl cambio, no lo evites. para que sean fácil de cambiar las cosas.
- También "O" de SOLID -> abierto a expansion pero cerrado para modificaciones

## Evita futuras rupturas

- Los test que hacemos van encaminados para eso.Evitar deudas técnicas.
- Preveer todos los fallos futuros o por lo menos sean fáciles de localizar.
> El mejor código es el que no se escribe

## Clean code: código limpio
Principio basico es que el codigo debe estar limpia no debe tener comentarios, ya que los comentarios van en los mensajes de commit.
- Una sola  responsbailidad tambien en funciones, en bucles, aplicarlo a todo lo que pueda.
- Seguir la semántica de los tipos de datos. Usar el tipo de datos mas adecuado. 

## Ejemplo en Raku

```raku

```

## Las excepciones son parte de la aplicacion
Son parte de una aplicacion y hay que diseniar las excepciones con tipos.
Son parte también de las HUs.

Ejm: HU6: Iris quiere poder recuperar todos los issues de un milestone. Si no hay ningun issue, se considerara el estado erroneo.

siempre debo tener las excepciones diseniadas y tambien las debo testear.Ya que en la historia de usuario me vva a decir quiero que me avise de estas cosas.
## Excepciones en Python: en el mismo fichero
```python
class NoIssueException(Exception):
  def __init__(self,*args,**kwargs):
    Exception.__init__(self,"Milestone sin issues")
```

## TODO: hito 6

- Modificar las HUs para que incluyan excepciones.
- Empezar a diseñar las clases usando estas técnicas.
- Comenzar implementación defensiva incluyendo excepciones
- Es lo menos habitual dentro de la ensenianza de la programacion. Entonces empezar a diseniar las excepciones. Tenerlas en cuenta dentro de las historias de usuario y segundo explicitamente buscando cuales son las mejores practicas para programar excepciones dentro del lenguaje que estemos.
si existe clase base que forme parte del core del lenguaje.
- Dentreo del fichero agil.yaml agregar lo siguiente:
Una clase `excepciones` que va a ser un array con uno o mas ficheros donde hayamos puesto las excepciones. El sistema va a comprobar que existe ese fichero.

```yaml
excepciones:
  -lib/X/Project/NoSuchIssue.pm6
```