# 3. Resolviendo problemas usando la informatica - hito 3

[Video](https://www.youtube.com/watch?v=0PxemjYKEAY&feature=youtu.be)
[Presentación](https://jj.github.io/curso-tdd/preso/aplicaciones)
[Material](https://jj.github.io/curso-tdd/temas/aplicaciones)
[Hito](https://jj.github.io/curso-tdd/temas/aplicaciones#actividad)

** Las multiples formas del software**

## RETRO: Repaso de lo que se debe hacer hasta ahora:

- Equipos organizados y PR aceptado.

**Test para el hito1**

1. Se ha formulado correctamente el problema?
   Se debe identificar primero el problema.
   Pensar que problema quiero resolver.
   Crear las épicas y estas epicas se dividen en historias de usuario.

## Software moderno

El MVP pasa por diferentes fases antes de llegar al producto final.

## Los modulos tambien son software

Hay que tener en cuenta los modulos, que son modulos, bibliotecas, librerias, clases, gramaticas, conjunto de funciones, se agrupan al rededor de una estructura de datos sean o no clases.
Una solución puede consiste perfectamente en una libreria, que se va a publicar en un repositorio de biblioteca. Ejm, publicar en nom, en python, en raku.
Muchas veces la gente siempre piensa en una aplicacion o en una solucion.

No pensar en que voy hacer un API rest que haga tal cosa, sino decir voy a crear una librería que resuelva un problema.

Las librerías son un producto mismamente viable.

Modularized es esencial. siempre se va atacar una épica, esta tiene varias historias de usuarios, debe siempre estar modularizarla. 

## APIs, papis

Interfaces de programación, formas de interactuar con una biblioteca. Técnicamente es un patron que se llama `decorador` para una biblioteca, lo que hace es esconder una lógica de negocio y la ofrece con un determinado protocolo estándar.
Un API tiene siempre tener por debajo una biblioteca o lib.
Interactuar entre partes de una aplicación.

> Parte de la programacion moderna y agil es crear todo de forma desacoplada

Hay muchos tipos de API:

- REST (usa semántica http) se usa mucho
- WebSockets: son muy interesantes
- GraphQL: es como rest con esteroides. Es un lenguaje de query para grafos te da un solo endpoint y sobre ese usa un lenguaje especifico. Tienes que tener una lib graphql que te interprete.
Trabajar siempre con mejores practicas.

Al final todos tienen endpoints.
Siempre hay que trabajar con mejores practicas.

Seccion millenials:

- SOAPL: protocolo
- OSGi:ex compleja usa xml y esta relacionado con java
- XML-RPC: simplifica SOAP
- gRPC: g de Google, pero con disimulo, es muy popular.

## Sistemas de mensajería

La gente ve poco, pero hay sistemas importantes como sistemas de colas. Sistemas en los cuales tu enviás un mensaje y tienes garantizada su recepción y luego hacer cosas con los mensajes.
Ventajas que tienes mensajes tipo broadcast, también los puedes ver un poco como llamada diferidas de un API, el mas popular es AMQP(Advanced Message Queuing Protocol), hay otros como XMPP que es el protocolo de mensajería que se usa en YAML.
Hay otros mas especificos XMQP.

## Seccion variedades

Al final se debe tener algo que use el usuario

### Scripts y CLIs

Es fenomenal y super comodo, se puede automatizar, facil de pasar parametros.
Se pueden poner delante de un API o solos. Incluso hay herramientas que te permiten hacer un TUI(terminal user interface), que puedes meterlo todo en el terminal, con emojis.
Hay clientes de GitHub, clientes de travis, de heroku o aws.

### Aplicaciones de escritorio
- Interfaz grafica como QT, ionic, electron, flutter.

### Aplicaciones MVC o cliente/servidor
Ventajas qtienes que son simples tienen framework muy simples, como django, laravel, synfony.
El problema es que siquieres hacer algo nuevo y bueno tienes que desacoplar las diferentes partes.

> Huir de esto como la peste. si se quiere usar esto entonces dividirla en un API, luego en un cliente, etc

### Aplicaciones basadas en microservicios

Es lo mejor ya que son muy modernas, son todas las riquezas de computación en la nube de hoy en dia. Tienen una forma de diseñar muy especifica, la ventaja es que pueden sacar productos mismamente viables continuamente. Es muy probable que si vas a trabajar en una aplicacion nueva al final vas a tener una app basada en microservicios.

## RETRO: Donde estamos ahora

- hito1: Haber planteado un problema
- hito2: Debemos haber elegido resolver un problema 
- y Porque estapas va a pasar.

Casi siempre se va a tener que pasar por estas 3 etapas, primero el MVP va a ser una libreria, el segundo producto minimamente viable sera una API que se ponga sobre ese modulo, 3er MVP posiblemente va a ser un cliente para ese API.
> Hay una herramienta Hooks que don un tipo de aplicacion que se activan cuando se hace una petición a un API o se recibe algun argumento de un API. Bots de telegram son un ejemplo de Hook.

Ejm: El que hagamos un bot de telegram, no significa que vayamos hacer solo un bot de telegram, sino tenemos que hacer una logica de negocio, luego hacer un API por encima que traslada los comandos de telegram a esa logica de negocio, y finalmente lo que se debe hacer es engancharlo con telegram.

El profesor propone entablar una discusión en el tablero kanban del proyecto y el resultado se describa en el README.md

En este hito3 el README.md tiene que decir queremos resolver este problema y lo vamos a resolver mediante este tipo de aplicacion, ejm: bot de telegram, API, Hook de github, etc y esa aplicacion la vamos a dividir en diferentes hitos la cual sera, la logica de negocio, segundo un API, y el tercero un cliente.
