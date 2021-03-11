# Calidad en un aplicación desde el diseño.

[Material](https://jj.github.io/curso-tdd/temas/dise%C3%B1o)
[Presentación](https://jj.github.io/curso-tdd/preso/dise%C3%B1o)
[video](https://www.youtube.com/watch?v=S1PCuyid-rw&feature=youtu.be)
[Hito](https://jj.github.io/curso-tdd/temas/dise%C3%B1o#actividad)

## Retro
- [x] Se formula correctamente el problema.
- [x] Se ha creado una épica
- [x] Proponer una solución informática
- [x] Proponer algún sistema de loggins y otros servicios 


## Tras la épica

Son las historias de usuarios, la HU como usuario necesito esto, como administrador necesito esto, como rol necesito lo otro.

Vamos hacer una serie de historia de usuario.s

Un hito es siempre un producto minimamente viable, un hito va a ser una epica la cual va necesitas varios hitos para terminarla.
historias de usuario, epicas y demas estan orientadas al disenio.

En este hito, vamos a deshacer la epica en las historias de usuario para que esas historias de usuarios.

Va a validar la existencia de una historia de usuario esencialmente un issue para empezar a programar.

## Disenio dirigido por dominio

A partir de las HU tenemos que identificar y tenerr un buen modelo del dominio del problema, por eso debemos siempe partir de un buen problema. 

> Si no tenemos problema no tenemos dominio del problema,  y si no tienes dominio del problema no puedes tener HU y no podemos acceder al disenio.

La tecnica DDD (Domandin Driven Desing), dentro de esto lo que debemos hacer es identificar 3 tipos de cosas o estruucturas de datos que son Objetos Valor, entidades y agregados.

**Objetos-valor**: son cosas que tienen un valor que en principio no tienen una gran entidad, son cosas que pueden tener diferente valor, pero que tienen poca autonomia y siempre existen dentro del contextto de algo que tengan un nivel de mayor gerarquia en este caso las entidades. Otra cosa es que son inmutables. Tienen sentido dentro de las entidades y ligeramente no van a tener sentido de forma independiente.
  
  `Objetos-valor -> Entidades`

**Entidades**: Las entidades son entidades dentro del Dominio del problema es decir son cosas que son identificables y autónomas aunque pueden tener dependencia de otras entidades pero al principio cuando tengo una entidad tengo algo que puedo trabajar con el que puede cambiar de valor. finalmente estas entidades van a estar dentro de AGREGADOS DE ENTIDADES. Normalmente una entidad no va a saber como gestionarse ni generarse a si misma, entonces necesita de agregados que tengan conocimiento de como generar estas entidades.

  `Entidades -> Agregados de entidades`

**Agregados**: van a incluir varias entidades, el nombre de este debe estar relacionado con el nombre de las clases o los objetos que agrega. Y si no tiene una gerarquia de clase determinada lo que va hacer es que creara diferentes directorios para reflejar esa estructura.
 

## Reflejarlo en el disenio de la jerarquia de clases o modulos.
Vamos  aseguir las mejores practicas del lenguaje de programacion. Debemos seguir las covnenciones con los nombres.
En este caso en algunos lenguajes de programacion un `objeto-valor` va a ser una deficion que este dentro de una clase cuya clase sera una entidad.
Siempre inentar que desde el principio la adquisicion de una serie de ids empiece a aplicar principios de disenios y de buenas practicas.

## Diseniar la estructura de datos correctamente.
Lo primero que se hace cuando se trabaja en cualquier proyecto es trabaar con las estructuras de datos. Tenemos que diseniar las estructuras de datos que capturen el dominio del problema. LA calidad empieza por el disenio, elegir una estructura de datos correcta permite ttrabajar con un lenguaje fuertemente ttipado y te ahorren muchas pruebas y test.

Las HU nunca tienen detalles de immplementacion.

## Activad para este hito 4
- Elaborar HU (dirigido a la persona que programa) una cantidad aceptable que permita crear a partir de ellas una serie de issues en Github. 
- Etiquetar las HUs con "HU", creando el label correspondiente en el repo de Github.
- Agregar el archivo agil.yaml

**HU go-notes**

Una app nos va apermitir registrar y mostrar las notas de las practicas de los alumnos de una materia. Mediante un 

>> El estudiante querra estar informado en todo momento de sus notas de cada una de las practicas de la materia.
Entidad: Materia - Practica - Nota- Estudiante
El agregado aqui integrara un API para dar acceso al estado de la Nota, ademas de permitir registrar MAteria y  practias, asi como notas. (Metodos, get, put, push)
Nota y estudiante seran los objetos-valore porque existiran dentro de una practica.


----
Problema: Almacenar las notas en diferentes prácticas de una asignatura, junto con comentarios adicionales y posibles anotaciones que se hayan podido hacer sobre las mismas.

Solución: Crear un API REST en el cual el docente pueda publicar las notas de sus alumnos junto a sus comentarios y anotaciones respectivos. Estas notas serán publicadas para que los estudiantes puedan revisarlas en cualquier momento mediante una web estatica.

-----

**Resolucion**  de las posibles clases o entidades/objetos-valor/agregados

*ASIGNATURA:entidad
  - Nombre

*PRACTICA:entidad
  - id
  - Nombre
  - Descripción
  - NOTA
  - Comentarios

*NOTA:objeto-valor

*MAIN:agregado
  - new
  - edit
  - delete
  - estado