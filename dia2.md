# 2. Desarrollo Agil

[Video](https://www.youtube.com/watch?v=qI5eowKJ9Ng&feature=youtu.be)
[Material](https://jj.github.io/curso-tdd/temas/%C3%A1gil)
[Presentación](https://jj.github.io/curso-tdd/preso/)
[Material adicional](https://agilemanifesto.org/iso/es/manifesto.html)

Buscar siempre las mejores practicas y tomar las mejores decisiones

- Ver commits

Una retro para revisar que ha sucedido con el hito anterior.
Revisar el trabajo en "retros" y en los PRs, lo mejor es revisar el código de otra gente. No confiar mucho en tutoriales para resolver un problema, para eso mejor voy a github y busco código que use tal librería, y lo reviso y si encuentro un error le envío un PR.

La version del PR debe coincidir con un tag del repositorio del proyecto.

## Manifiesto agil
Tiene una serie de lemas:

- Documentación y + codigo funcionando: No preparar una monton de documentacion ya que lo que mas importa es el código funcionado.

- Procesos + interacción con cliente: Interacción todo el tiempo, interaccion-codigo-retroalimentacion-codigo y entrega a cliente.

- - contratos + colaboracion: Mas colaboracion entre las personas, preguntar es esto lo que me has pedido, y asi colaborar entre todos.  

> Lo importante siempre es el codigo funcionando

Estos lemas organizan una serie de principios:

- Resolver problemas: el software de hace para resolver problemas, ya que tu tienes que resolver el problema de tu cliente. Lo esencial es que debes partir el problemas, debes plantear la solucion que vas hacer en terminos de que es lo que vas a resolver. ejm: Quiero resolver que los estudiantes tengan acceso a una asignatura de una forma facil.

- Publicar frecuentemente: pasar siempre los productos minimamente viables, ya sea cada semana, pasando a produccion cualquier cosa que este lista y pase todos los tests. cada hito debe tener un producto minimamente viable, hay que ordenar el proyecto en hitos.

- Buenas practicas y buen diseño: es esencial y es donde se hace mas enfasis. El diseno previo a la codificación debe seguir todos los lemas y principios agiles y buenas practicas.

- La simplicidad es esencial:  no se debe hacer mas que lo que hay en los requisitos.ni buscar mas caracteristicas que las estrictamente se necesiten para resolver un problema. HAcer un producto minimamente viable. Solo hacer el codigo necesario para pasar los tests. Herramientas con los que todos esten familiarizados.

- Revisar el trabajo frecuentemente: con el objetivo de hacerlo mas eficiente, cada dia hacer una retro. adaptarlo a nuevos requisitos o simplemente incorporarlo a produccion. El codigo siempre debe pasar por varios ojos.


**La calidad empieza en el diseño:** Es importante, un ejm: como vamos a diseñar las clases, como va a ser la lógica de negocio, que tipos de datos vamos a utilizar para esa clase, el tipo de datos infiere en la velocidad y como va a interactuara. 

LAs 2 o 3 clases siguientes vamos a trabajar en esa parte del diseño.

**Buscar siempre las mejores practicas en cualquier decision técnica:** La sintaxis, manuales de referencia, En cada momento buscar cual es el codigo o biblioteca que resuelve mejor tu problema. No llevar nunca una idea fija.

**Infraestructura para revisar codigo y el trabajo en "retros" y en los PRs:** Lo mas simple es estableces un estandar en el cual no se incorporte codigo a la rama principal directamente, sino que se haga siempre mediante PR. Adicionalmente, el desarrollo agil pide la creacion de una serie de reuniones, normalmente llamadas retro, que revisan el codigo que ha puesto en produccion, y sugiere, siempre de forma costructiva, diferentes mejoras (que se incorporaran a un MPV futuro). El pasar test frecuentemente para guardarse de posibles cambios en las dependencias tambien es una buena practica, porque cerrarse en una version determinada de todo puede ser eficiente.

## Como vamos a resolver el problema

### Historias de usuario
**Los deseos de los clientes**
Que es lo que los usuarios quieren que soluciones.

Varias historias de usuario relacionadas se agrupan en **épicas**

Como son las historias de usuarios.
> Como usuario de tipo x, en el contexto y, quiero que suceda z, y sino, w.

Como hacemos esto en la practica?

### SCRUM o Kamban?

Son 2 metodologias agiles por excelencia, y suelen mezclarlas.

Vamos a usar el tablero Kamban como el del curso, con las siguientes columnas.

En github creamos un proyecto y como template elegimos el tablero kamban automatizado, que se crea con 3 columnas
- A consideración (esta columna podemos crear)
- Todo: cuando llegan a esta coluna ToDo, estas fichas se convierten en Issues y esos issues van a ser historias de usuario es decir como problema a resolver.
- In Progress
- Done

### Problema
- Cual va ser el hito1, lo esencial es decidir que problemas quieres resolver.
- Crear nu proyecto en el repo para organizar las tareas. Podemos crear una columna, en la qe podamos agregar ideas y conversar dentro de esas tarjetas de ideas. Siempre es importante qe todo el equipo este de acuerdo en el problema a resolver.
- Un hito consigue un produucto minimamente viable.

- Diseniar una epica que guie el desarrollo, que es na narrativa e incluya muchas historias de usuario.

Siempre trabaja con historias de usuarios que son issues

BDD - behavioral driven development, resolver problemas como una narrativa como una historia.

La épica es que es lo que quiere la persona.
