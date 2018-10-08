# React Context API
Slides de mi lightning talk "React Context API".

Hecha con [Reveal.js](https://github.com/hakimel/reveal.js).

---
# __Código escrito en Live Coding__

Este es el código escrito en la parte de Live Coding, con muchos comentarios para explicar cada parte de cómo se utiliza.

**App.js**
```javascript
import React, { Component } from "react";
import logo from "./logo.svg";
import "./App.css";

//Creamos el contexto
const MiContexto = React.createContext();

//Creamos un provider para nuestro contexto
class MiProvider extends Component {
  //Definimos un state que podemos compartir
  state = {
    nombre: "Bobby",
    edad: 5
  };
  render() {
    return (
      /*
        Mandamos por el atributo 'value' del Provider todo lo que querramos
        compartir en el contexto
      */
      <MiContexto.Provider
        value={{
          state: this.state,
          /*
            Podemos compartir también funciones!
          */
          sumaruno: () => {
            this.setState({ edad: this.state.edad + 1 });
          }
        }}
      >
        {this.props.children}
      </MiContexto.Provider>
    );
  }
}

const Animal = props => (
  <div className="family">
    {/*
      Seguimos con el prop drilling
    */}
    <Perro dato={props.dato} />
  </div>
);

class Perro extends Component {
  render() {
    return (
      <div>
        {/*
          Definimos el consumer para poder consumir la data pasada por value
        */}
        <MiContexto.Consumer>
          {context => (
            <React.Fragment>
              <h6>Cosas por context</h6>
              <p>El nombre de mi perro es {context.state.nombre}</p>
              <p>Y tiene {context.state.edad} años</p>
              {/*
                Acá usamos la función sumaruno recibida por context!
              */}
              <button onClick={context.sumaruno}>Sumar años</button>
            </React.Fragment>
          )}
        </MiContexto.Consumer>
            
          {/*
            También podemos seguir compartiendo cosas por props,
            solamente que tenemos que usarlas fuera del Consumer  
          */}
        <h6>Cosas por props</h6>
        {this.props.dato}
      </div>
    );
  }
}

class App extends Component {
  render() {
    return (
      //Utilizamos el provider en el componente más alto posible de nuestro programa
      <MiProvider>
        <div className="App">
          <header className="App-header">
            <img src={logo} className="App-logo" alt="logo" />
            {/*
              Podemos seguir mandando data por props
            */}
            <Animal dato="Recibido por props" />
          </header>
        </div>
      </MiProvider>
    );
  }
}

export default App;
```

---

# __Instalación__

Desde el directorio principal `npm install && bower install`

---

# __Utilización__

Una vez que está todo instalado, `grunt serve` inicia el proyecto localmente

---

# __Créditos__

[Yarn HTML Presentation](https://github.com/ibbatta/yarn-presentation (utilizada como base))

En los slides se incluyen créditos adicionales.