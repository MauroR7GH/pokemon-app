# Pokemon App

<p align="left">
  <img height="150" src="./pokemon.png" />
</p>

## Podes probar la app con el siguiente link

- 馃寧 Deploy: https://pokemon-app-henna.vercel.app

## Objetivos del Proyecto y algunas imagenes

- Construir una App utlizando React, Redux, Node y Sequelize.
- Aprender mejores pr谩cticas.
- Aprender y practicar el workflow de GIT.

<img src='./client/src/img/Landing.png' width='350px' align='left'/>
<img src='./client/src/img/Home.png' width='350px' align='center'/>
<img src='./client/src/img/Details.png' width='350px' align='left'/>
<img src='./client/src/img/Create.png' width='350px' align='center'/>

## Comenzando

 1. Forkear el repositorio para tener una copia del mismo en sus cuentas
 2. Clonar el repositorio en sus computadoras

__IMPORTANTE:__ Es necesario contar minimamente con la 煤ltima versi贸n estable de Node y NPM. Asegurarse de contar con ella para poder instalar correctamente las dependecias necesarias para correr el proyecto.

Actualmente las versi贸nes necesarias son:

 * __Node__: 12.18.3 o mayor
 * __NPM__: 6.14.16 o mayor

Para verificar que versi贸n tienen instalada:

> node -v
>
> npm -v

## BoilerPlate

El boilerplate cuenta con dos carpetas: `client` y `server`. En estas carpetas estar谩 el c贸digo del front-end y el back-end respectivamente.

En `server` crear un archivo llamado: `.env` que tenga la siguiente forma:

```
DB_USER=usuariodepostgres
DB_PASSWORD=passwordDePostgres
DB_HOST=localhost
PORT=3001
```

Reemplazar `usuariodepostgres` y `passwordDePostgres` con tus propias credenciales para conectarte a postgres.

Adicionalmente ser谩 necesario que creen desde psql una base de datos llamada `pokemon`

El contenido de `client` fue creado usando: Create React App.

## Enunciado

La idea general es una aplicaci贸n en la cual se puedan ver los distintos Pokemon utilizando la api externa [pokeapi](https://pokeapi.co/) y a partir de ella poder, entre otras cosas:

  - Buscar pokemons
  - Filtrarlos / Ordenarlos
  - Crear nuevos pokemons

__IMPORTANTE__: Para las funcionalidades de filtrado y ordenamiento NO se utilizaron los endpoints de la API externa que ya devuelven los resultados filtrados u ordenados sino que est谩n construidos propiamente en la aplicaci贸n.

### 脷nicos Endpoints/Flags externos usados

  - GET https://pokeapi.co/api/v2/pokemon
  - GET https://pokeapi.co/api/v2/type

### Requerimientos m铆nimos:

__IMPORTANTE__: Para aplicar estilos a la aplicaci贸n se utilizo CSS Modules.

#### Tecnolog铆as necesarias:
- React
- Redux Toolkit
- Express
- Sequelize - Postgres

## Frontend

La aplicaci贸n contiene las siguientes pantallas/rutas.

__Pagina inicial__: una landing page con bot贸n para ingresar al home (`Ruta principal`)

__Ruta principal__: contiene
- Input de b煤squeda para encontrar pokemons por nombre (La b煤squeda es exacta, es decir solo encontrar谩 al pokemon si se coloca el nombre completo)
- 脕rea donde se ve el listado de pokemons mostrando su:
  - Imagen
  - Nombre
  - Tipos (Electrico, Fuego, Agua, etc)
- Botones/Opciones para filtrar por tipo de pokemon y por pokemon existente o creado por el usuario
- Botones/Opciones para ordenar tanto ascendentemente como descendentemente los pokemons por orden alfab茅tico y por fuerza
- Paginado para ir buscando y mostrando los siguientes pokemons, 12 pokemons por pagina.

__IMPORTANTE__: Dentro de la Ruta Principal se muestran tanto los pokemons traidos desde la API como as铆 tambi茅n los de la base de datos. Por otro lado, para traer la informaci贸n de los pokemon fue necesario hacer un subrequest y obtener los datos necesarios desde ah铆. Debido a que esto puede hacer que la b煤squeda sea muy lenta se limit贸 el resultado total a 40 pokemons provenientes de la API externa.

__Ruta de detalle de Pokemon__: contiene
- Los campos mostrados en la ruta principal para cada pokemon (imagen, nombre y tipos)
- Estad铆sticas (vida, fuerza, defensa, velocidad)
- Altura y peso

__Ruta de creaci贸n__: contiene
- Un formulario __controlado y validado con JavaScript__ con los campos mencionados en el detalle del Pokemon
- Posibilidad de seleccionar/agregar m谩s de un tipo de Pokemon
- Bot贸n/Opci贸n para crear un nuevo Pokemon

## Base de datos

El modelo de la base de datos tiene las siguientes entidades:

- Pokemon con, en principio y por el momento, las siguientes propiedades:
  - ID
  - Nombre
  - Vida
  - Fuerza
  - Defensa
  - Velocidad
  - Altura
  - Peso
- Tipo con las siguientes propiedades:
  - ID
  - Nombre

La relaci贸n entre ambas entidades es de muchos a muchos ya que un pokemon puede pertenecer a m谩s de un tipo y, a su vez, un tipo puede incluir a muchos pokemons.

## Backend

Est谩 desarrollado un servidor en Node/Express con las siguientes rutas:

- __GET /pokemons__:
  - Obtiene un listado de los pokemons desde pokeapi y desde la base de datos.
- __GET /pokemons/{idPokemon}__:
  - Obtiene el detalle de un pokemon en particular a partir de su id
- __GET /pokemons?name="..."__:
  - Obtiene el pokemon que coincide exactamente con el nombre pasado como query parameter (Puede ser de pokeapi o creado por nosotros)
- __POST /pokemons__:
  - Recibe los datos recolectados desde el formulario controlado de la ruta de creaci贸n de pokemons por body
  - Crea un pokemon en la base de datos
- __GET /types__:
  - Obtiene todos los tipos de pokemons posibles
