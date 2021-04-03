# Inyección de dependencias (hito12)

[Material](https://jj.github.io/curso-tdd/temas/inversi%C3%B3n#Actividad)
[Video](https://www.youtube.com/watch?v=VjZhMr1DB3k&list=PLsYEfmwhBQdJJsCTshZw8Ae67lU48wkaA&index=14)
[Presentación](https://jj.github.io/curso-tdd/preso/inversi%C3%B3n.html)


Inversion de dependencias, mocks, y cosas similares. Veremos como se integra esto en ciertos patrones de programación que se suelen usar en tests.

## TODO
[x] Los milestones internos son productos minimamente viables
[x] Se han integrad tests en el gestor
[x] Se ha integrado un sistema de CI

## Retro

Los problemas con .yaml es mas común en su sintaxis.

[] Hay espacios en blanco en la ultima linea de un YAML

Configurar el editor de código para revelar los espacios en blanco al final de la linea.


## Roles => inversion de dependencias => mocks

La intención final es que aprendamos a hacer mocks y como trabajar con ellos.

Vamos a seguir esta ruta:
- Roles
- Inversion de dependencia: principio de programación ágil y principios SOLID, desacoplamiento de las diferentes funcionalidades
- mocks, concepto general, etc.

> Acostumbrarnos a que cuando vayamos a una empresa debemos trabajar conn diferentes lenguajes de programación. Tenemos la posibilidad de aprender lenguajes de programación rápidamente. Una habilidad es entender que hace el programa sin entender el lenguaje de programación. Ser capaces de ver ejemplos de lenguajes de programación y entender el concepto de lo que se quiere hacer.

## Roles: Composición frente a herencia

En POO sabemos los principios, encapsulation, herencia,`principio de sustitución de liskov` => _esto dice que podemos usar cualquier objeto que este dentro de una jerarquía de clase siempre y cuando este dentro de la jerarquía de clase_. 
Perro esto no solo se puede lograr con herencia sino también con composición. 
La idea de la `composición` es que tu creas ese objeto no heredando uno de otro como una gerarquia sino componiendo varias partes de un objeto para crear otro objeto, esto cumple el principio de sustitucion de liskov para cada una de las partes. 

Al final esto se llaman de diferentes formas: _roles_, _mixins_, _aspectos_, son aprecidas a la genericidad (clase generica).

**Roles son "clases incompletas"**: lo que tienes o puede tener atributos, funciones, instancias o sin instanciar o puedes tener todo. En java a esto se le llama `interfaces`

Roles, pequeños comportamientos o funcionalidades para crear una clase, y va a ser sustituible por las clases que componen esos roles.

Ejemplo -> Roles = modulos en Ruby
```ruby
module Named
  attr_reader :name
end

class Project
  include Named
  attr_reader :issues, :milestones, :logger

  def initialize(name,logger)
    @name = name
    @issues = []
    @milestones = []
  end
# .. mas
end
```
Este uso de roles es lo esencial cuando se trabaja con inyección de dependencias o mocks.

## Inyectando dependencias: usando roles
Abstraen la funcionalidad que quieres que haga esa depedencia y desacoplas la dependencias de la implementación del objeto.

Lo que voy hacer es crear un objeto que componga esas funcionalidades y esto lo logramos haciendo roles, tenga o no el lenguaje de programación roles, sino los tiene habría que usar binding dinámicos de método a objetos o lo que sea.

La idea de rol es que la dependencia eterna va a tener esta funcionalidad.

## Desacoplando diferentes funciones
La programación ágil es ese desacoplamiento de las diferentes partes, que te permite testear y desarrollar de forma independiente y sobre todo permite evolucionar el código a base de desautorizaciones de forma independiente.

**Las dependencias son atributos**

```raku
unit class Project::Stored does project;

has Project::Dator $!dator;

//rol::atributo
```

## Dobles de test: sustituyen a objetos originales

Esto es un concepto mas amplio que el de mocks, hay dobles de test que no son mocks. Son dobles como en el cine.

Sustituyen a objetos originales, mostrar o imitar comportamiento de los objetos originals porque son caros o por seguir FIRST.

> Recordad: Debemos usar la inyección de dependencia cuando vayamos a trabajar con cualquier tipo de dependencia externo, ejemplo un logger, siempre vamos a tener que trabajar con logger y la inyeccion de dependencias es un target impresindible cuando se trabaja con logger, bases de datos, incluso se hacen mocks del tiempo y hora.

Hay muchos tipos de mocks que se diferencias de la funcionalidad.
- dummies mocks: no tiene funcionalidad
- Stubs: son como dummys pero tienen interface, tienen algo mass de funcionalidad.
- Fakes: clases falsas, tiene cosas generadas estaticamente o devuelven siempre lo mismo.

## Mocks: cualquier imitador de funcionalidad

Realmente los frameworks ayudan a crear esos mocks, pero no son exclusivos.
Necesitass tener claro el disenio ppara saber esa inyeccion de dependencia y entender el cocepto de rol para que te ayuden a crear los mocks.

## TODO Hito 12

- Implementar algún tipo de inyección de dependencia, por ejemplo como forsozamente tenemos que usar logs, debemos usar en las clases de loggin, en muchos lenguaje de programacion tenemos frameworks de loggin apra poder usar vario tipos logs. 
Programar inyección de dependencias, para  con logs e integrar algun tipo de servicios. Comenzar a integrar los servicios por inyección de dependencias.
- Integrar los test correspondientes.
- Se usara el checks API para comprobarlo