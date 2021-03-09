# Servicios avanzados en informática - hito4

[Material](https://jj.github.io/curso-tdd/temas/servicios)
[Diapositivas](https://jj.github.io/curso-tdd/preso/servicios)
[Video](https://www.youtube.com/watch?v=VMfaNvTVq5w&feature=youtu.be)
[hito](https://jj.github.io/curso-tdd/temas/servicios#actividad)

https://www.confluent.io/blog/turning-the-database-inside-out-with-apache-samza/

## Retro: En donde estamos
[x] hito1: Se ha formulado el problema correctamente?
[x] Se ha creado una épica
[x] Se ha propuesto una solución informática


## Hay servicios imprescindibles en una aplicacion

Cuano se piensa en una aplicacion se piensa en cosas que son impresindibles, por lo menos cuando se trabajan en apps nuevas que se desarrollan en la nube, se describen los servicios que son imprecindibles.

### Logs
El servicio mas util de que talvez no has oido hablar es el de loggins o registro.
Los logs son esas cosas que uno pone para enterarme por donde va, en apps distribuidas y en la nube son imprecindibles totalmente a todos los niveles, porque son apps complejas que tienen diferentes instancias, diferentes componentes, nodos, diferentes contenedores, y se debe tener una vision centralizada. Las aplicaciones tienen que tener una caracteristica que es `observabilidad` y esata tiene que estar en los logs. Es mucho mas facil que si se la aniade al incio que aniadirla al final. Porque incluso se puede aniadir un tipo de middleware que cada vez que pase un evento del sistema, como crear un objeto o evento significativo, tenemos que saberlo, esto es para que en caso de error saber en donde se ha quedado.

Tienen algo curioso es que si tienes los logs detallados del sistema, puedes saber el estado actual del sistema.

**Arquitectura Kappa** esta basada en los logs, que en vez de meter cosas en la base de datos, lo que hace es usar log, querys al log, se ayuda de herramientas que se llaman Kafka y herramientas especcificas para trabajar con estos, esta basada en mensajes, en strings.

Se puede usar con **Librerias basicas o externas** dependiendo del lenguaje de programacion.
Tiene librerias para escribir y leer los logs. Se puede usar librerias o servicios externos.

Que servicios externos hay? de pago como [logz.io](https://logz.io/) o libres como [logstash](https://www.elastic.co/guide/en/logstash/current/logging.html) tienen una cosa que no es exacatamente libre, lo que haces es que te levantas un servicio de logstash lo configuras y le mandas peticiones y sacas por pantalla o fichero o poderle decir que lo almacene en elastic o stack kibana.

Ejemplo de loggins en Rust:

```rust
use simple_logger::SimpleLogger;

#[derive(Debug)]
pub enum IssueState {
    Open,
    Closed,
}

#[derive(Debug)]
pub struct Issue {
    state: IssueState,
    project_name: String,
    issue_id: u64,
}

pub fn issue_factory( project_name: String,
                      issue_id: u64) -> Issue {
    log::debug!( "Creating closed issue for project {} with id {}", project_name, issue_id );
    return Issue { state: IssueState::Closed,
                   project_name: project_name,
                   issue_id: issue_id }
}

fn main() {
    SimpleLogger::new().init().unwrap();
    let this_issue = issue_factory(String::from("CoolProject"), 1 );
    let mut that_issue = issue_factory( String::from("CoolProject"), this_issue.issue_id + 1 );
    that_issue.state = IssueState::Open; // Avoid warning
    log::debug!("Changed state to Open");
}

#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn check_creation() {
        assert_eq!(issue_factory(String::from("CoolProject"), 1 ).issue_id, 1);
        assert_eq!(issue_factory(String::from("CoolProject"), 1 ).project_name, "CoolProject");
    }
}
```

Rust no es Orientado a objetos. Tiene algo que se llaman las factorias en vez de tener un constructor para un objeto. En este ejemplo el programa crea issues de un proyecto.
Es importante testear tambien los logs.

### Configuracion remota
Otro servicio muy importante también y que no se suele conocer es la configuración remota. 
En una app y forma parte de algo que se le conoce como `los 12 pasos` es que la configuración este en el entorno. Nunca se debe anteponer nada que sea configuración de una app como el propio código, sino que tiene que estar como parte del entorno. Es decir tiene que estar en una variable de entorno, pasarlo por un CLI o finalmente usar un sistema de configuración remota.

Los sistemas de configuración remota, que hacen? tienen un puerto de acceso que es un puerto conocido, que solo tienenes que usar un driver para acceso remoto y aveces tienes que ponerle clave, pero sino le pones, puedes hacerle peticiones de cosas, clave valor. Tu almacenas esas claves y valores cuando arranca la aplicacion y cada vez que se levanta la app lee el sistema de configuracion remota. Un servicio de tercero para configuracion remota es [etcd](https://etcd.io/) hay otros incluso especificos del lenguaje. Hay otros como [consul](https://www.consul.io/) que tambien incluyen un almacen clave valor que puede usar para almacenar la configuracion remota, esta escrito en erlang, podes instarlo con un docker.

Aconseja el uso **etcd**

### Almacenamiento de datos
- Hay muchas formas de almacenar datos, estamos pensando mas o menos en servicios avanzados, postgressql, mongo, mysql. 
SGBD con SQL.
- Hay bases de datos documentales como elastic, mongdb, kasandra, como Riak como couchdb. 
Tambien puede servir un Json, con esquema sin esquema, luego como lo recupero?
Hay muchas bases de datos documentales. Si acaso estoy usando elastic con logstash para el logging, ps hago otro espacio de docuemnto para la base de datos y listo y asi reuso elastic.

- Hay sistemas **clave-valor**, un ejemplo es `etcd` relativamente simple, pero hay unos mas complejos que permiten almacenar estructuras de datos mas complejas, uno bien conocido es Redis que es una BD clave-valor que esta en memoria y es persistente, esta escrita en C, van super rapida, tambien se puede usar para sistemas de mensajeria, y tiene un monton de clientes.

- Bases de datos en **tiempo real**, se pueden usar como log, lo esencial es que todas las entradas tienen un sello de tiempo, las busquedas estan enfocadas en temporales, ejmplos son RethingDB, Firestore, son utiles si necesitas una linea de tiempo.

- **Grafos**, gran cantidad de informacion se puede almacenar de forma natural en grafos. En un grafo tu accedes a un nodo y vas acceder a nodos que esten relacionados con ese nodo, en primero orden, segundo orden, etc, todas las conexiones que hay con un node, aqui no va hacer busquedas con una clave, no va hacer un join de esos con 2 calves lo que interesa es acceder a todos los followers de una persona, o quiero acceder a todos los links de una persona. Las BD de grafos son utiles para expresar relaciones entre cosas y puede ser util para guardar cosas como datos RDF sujeto-vervo-predicado, sujeto, el verbo es el enlace y el predicado es otro nodo que hay, tienes diferentes nodos relacionados con diferentes predicados. La mas famosa es Neo4J.

- Los sitemas de ficheros son excelentes y estan ahi, tienen formas de hacer log a nivel de directorio, a nivel de fichero, lo veremos mas adelante en un ejemplo, podemos organizar una base de datos arbolescente solo usando sistemas de ficheros y eso va a ir como las motos, no importa en el sistema, muchos de estos sistemas de archivos permiten almacenar metadatos junto con los ficheros y los mas obvios osn la fecha.
Hay sistemas de ficheros comerciales como Hadoop, HDGS, hay algunos para tipos de cosas determinadas, algunos como S3, que sirven para almacenar ciertas cosas. Una de las cosas que se debe tener en cuenta es que cuando vayas hacer una aplicacion no vay a tener un solo almacen de datos, sino vaya a tener varios almacenes de datos.

### Servidores Web

- Nginx: Se pueden usar juntos, es algo que tu no vas a tomar en cuenta la app pero sicuando disenias la arquitectura de la app, cuando disenias un API por ejm. si el manual dice que no lo uses para produccion, entonces no lo uses para producción.
- Lite httpd
- Gunicorn

### Sistemas de mensajeria

- RabbitMQ es un servicio de mensajeria, en conjucion con Celery. Si quieres tener una arquitectura distribuida debes tener un servicio de mensajeria. 


## Que vamos hacer como actividad en este hito

Que servicios vas a usar y porque es un logger?
Considerar el resto de los servicios para mas adelante.

