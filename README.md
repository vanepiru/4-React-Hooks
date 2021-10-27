***React Hooks***

Los Hooks son una API de la librería de React (a partir de 16.8) que nos permite tener estado, y otras características de React, en los componentes creados con una function. Esto, antes no era posible y nos obligaba a crear un componente con class para poder acceder a todas las posibilidades de la librería. Y de ahí viene el nombre Hooks es gancho y, precisamente, lo que hacen, es que te permiten enganchar tus componentes funcionales a todas las características que ofrece React.

***React Hooks, useState***

SIN HOOKS

 ![Sin título](https://user-images.githubusercontent.com/6796155/138974027-28b98662-b572-4475-9aef-c7d7e06a7062.png)



```js
import React, { Component } from 'react'

class Contador extends Component {
  state = { count: 0 } // inicializamos el state a 0

  render () {
    const { count } = this.state // extraemos el count del state

    return (
      <div>
        <p>Has hecho click {count} veces</p>
        { /* Actualizamos el state usando el método setState */ }
        <button onClick={() => this.setState({ count: count + 1 })}>
          Haz click!
        </button>
      </div>
    )
  }
}

CON HOOKS

```
Ahora, gracias a los hooks, podremos conseguir el mismo resultado utilizando una function e importando el hook useState de la siguiente forma:

https://codesandbox.io/s/v83v5mk1py?file=/src/Contador.js

```js
// importamos useState, el hook para crear un state en nuestro componente
import React, { useState } from 'react'

function Contador() {
  // useState recibe un parámetro: el valor inicial del estado (que será 0)
  // y devuelve un array de dos posiciones:
  //  la primera (count), tiene el valor del estado
  //  la segunda (setCount), el método para actualizar el estado
  const [count, setCount] = useState(0)

  return (
    <div>
      <p>Has hecho click {count} veces</p>
      { /* actualizamos el state al hacer click con setCount */ }
      <button onClick={() => setCount(count + 1)}>
        Haz click!
      </button>
    </div>
  )
}
```

***React Hooks, useEffect***

Características de useEffect

1.	Recibe dos parámetros: el primero una función y el segundo un array cuyos valores serán variables de las que depende nuestro efecto (este array es opcional).
2.	Se ejecuta en cada renderizado incluyendo el primero.
3.	Se puede usar más de un useEffect dentro de un componente.
4.	Está diseñado para que si la función que pasamos por parámetro retorna a su vez otra función, React va a ejecutar dicha función cuando se desmonte el componente.

*useEffect*: accediendo al ciclo de vida de nuestro componente. 

Ciclo de vida de un componente con class era fases de montaje, actualización y desmontaje.

Para ello usaremos useEffect, un hook que recibe como parámetro una función que se ejecutará cada vez que nuestro componente se renderice, ya sea por un cambio de estado, por recibir props nuevas o, y porque es la primera vez que se crea.

```js
import React, { useEffect } from 'react'

function Example() {
  useEffect(function () {
    console.log('render!')
  })
  
  return <span>This is a useEffect example</span>
}
```

Es lo mismo que 

```js
import React, { Component } from 'react'

class Example extends Component {
  componentDidMount () {
    console.log('render!')
  }

  render () {
    return (<span>This is a componentDidMount example</span>)
  }
}
```

Ejemplo

```js
import React, { useEffect, useState } from 'react'

function Contador() {
  const [count, setCount] = useState(0)

  useEffect(() => {
    // Actualiza el title de la página en cada click!
    document.title = `Has hecho clic ${count} veces`
  })

  return (
    <div>
      <span>El contador está a {count}</span> 
      <button onClick={() => setCount(count + 1)}>
        Incrementar contador
      </button>
    </div>
  )
}
```
https://codesandbox.io/s/948pj1q7kw

Funciona como el ciclo de vida componentDidMount y componentDidUpdate

