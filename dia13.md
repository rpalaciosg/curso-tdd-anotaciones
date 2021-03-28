# Integración/despliegue Continuo

[Material](https://jj.github.io/curso-tdd/temas/CI)
[Video](https://www.youtube.com/watch?v=97dnTC3RXAg)
[Presentación](https://jj.github.io/curso-tdd/preso/CI.html)

La idea es automatizar y poder trabajar automaticamente con los tesst y en general con todo lo que haga falta trabajar en la aplicacion.

## TODO
[x] Milestones
[x] Se han integrado los test en el gestor

## En busca del botón rojo de despliegue

La idea de programación agil, todo lo que va a la rama principal va a produc
ción, es decir no debe haber un proceso complicado pasar de los fuentes a la producción.

Si piensas hay diferentes procesos para asar un fuente a produccion como compilacion, transpilacion, generacion de codigo diversas, describir servicios que hay, desplegar servicios y finalmente desplegar la aplicacion. Se busca un mecanismo donde no haya integracion humana.

## Ganchos en la red / Hooks
Mecanismo generalizado de hooks. Son hooks que se conectan a repositorios.
Generaaalmente  los hooks son un API rest simple al que le envias un payload determinado, y ese payloaad determinado es tan facil como nombre de repositorio, token de autenticacion y nombre de repositorio.

Cualquier sitio recibe eso y dice entonces que es lo que tengo que hacer;
- descarga el repositorio usando git clone, normalmente hace un shallow-clone, es decir que no despliega toda la historia sino  un commit o  2 commits ultimos y a partir de ahi va haciendo las pruebas. 
Esto no es nada magico y es estandar, se lleva haciendo desde hace tiempo, primero se uso hansok, luego jenkins, y travis salio en 2014.

Todo esto lo puedes tener en servicios propios o privados.

## Configuracion generalmente en YAML

Es un formato de serializacion, tiene ciertos tipos, puedes crear un parse de yaml con bash.

### Infraestructura como codigo
Lo importante que la estructura y gestion de calidad debe tener la mentalidad devops que concuerda con mentalidad agil.

Esencialmente lo que le digo al sistema de integracion continua, oye mi sistema va a ejecutarse aqui, y quiero que me momentes un sitema y aqui voy a ejecutar los test.

## Travis

ejemplo:

```yaml
language: node_js
node_js:
  - "10"
  - "11"
  - "12"
before_install:
  - npm install -g mocha
install:
  - cd src; npm  install . //aqui podria llamar make install
script: cd src; mocha
```
El tutor lo aconseja y no lo aconseja, hasta ahora era open source friendly, pero  ahora ya es dificil para cosas open source.


Cuando hacemos integracion continua que hacemos:
- Primero seleccionamos el lenguaje, que es un runner determinado
- luego selecciono la verison del lenguaje
- luego instalamos dependencias
- luego ejecutamos los scripts


Entonces escribimos un archivo de configuración de travis que diga esto, y si no lo dice.
Una cosa interesante que hace travis es saber cual es la version minima con la que funciona tu aplicacion. Siempre poner las versiones LTS y la ultima.

Limitacion  de travis, es el credito.

> Un consejo para no gastar creditos al ahcer commit en el mensaje poner "skip ci" o "skip travis" por si en ese commit no quiero ejecutar los test
> cada vez que haga un commit no hacer push, el commit siempre debe ser atomico, y c usando ya este cansado ahi hago push

## Github actions FTW

Son for the wind xq tienen limitaciones. 
Son acciones, son un sistema de flujos de trabajo que tienen como arranque algún evento que suceda dentro del repositorio, o incluso fuera del repositorio.

- Le pones un nombre a la github actions.
- Luego tiene algo que puede filtrar por caminos,  tags, o paths especificos.
- Luego tiene diferentes jobs que son diferentes maquinas virtuales, si quiero que haya diferentes  ambientes de ejecucion, entonces necesito diferentess jobs. Cada job puede ejecutarse en una maquina virtual o un contenedor.
- Cada job tiene `steps`, es un array en yaml, y cada uno de los steps y puede usar algo que se llama github actions.
> Todas las actions/nombre son github actions del propio github
- LAs actions son flexibles, pueden estar escritas en perl, las oficiales estan escritas en typescript.

Ahora han sacado una cosa que se llama github script que esencialmente es typescript con una serie de objetos que te permiten acceder al API de github y también a todos los objetos de una github actions.

- Hay /setup-lenguaje@v1 son setups de versiones esepcificas de un leneguaje

Las Github actions no son rapidas F en F.I.R.S.T. si los test durran mas de 2 minutos la cosa empieza a ser fea. Tratar d eno perder el estado de flow.

# Hito 11
- Instalar sistema de CI y pasar los tests: github actions, travis, circleCI. PEdir que el sistema a usar usa checks API para comprobarlo.

## Solución
Agreguo archivo de github action `.github/workflows/CICD.yml`

```yaml
name: CICD
on: [push, pull_request]
jobs:
  test:
    strategy:
      matrix:
        go-version: [1.15.x,1.16.x]
        os: [ubuntu-latest, macos-latest, windows-latest]
    runs-on: ${{ matrix.os }}
    steps:
    - name: Install Go
      uses: actions/setup-go@v2
      with:
        go-version: ${{ matrix.go-version }}

    - name: Intall dependencies
      run: |
        go version
        go get -u golang.org/x/lint/golinto version
        go get -u github.com/stretchr/testify/assert

    - name: Checkout code
      uses: actions/checkout@v2

    - name: Run vet & lint
      uses: make check

    - name: Run testing
      run: make test

    - name: up code coverage
      - uses: actions/checkout@master
      - uses: codecov/codecov-actions@v1
        with:
          token: ${{ secrets.CODECOV_TOKEN }} # this is because is into organization 
          flags: unittests
      run: bash <(curl -s https://codecov.io/bash)

```