---
  title: Conhecendo o React-Native
  author: Kássio Luz
  date: 02/04/2019
---

Conhecendo o React-Native
--

###### Lista de Abreviaturas e Siglas
| Sigla         | Nome                       |
| ------------- |:--------------------------:|
| RN            | React-Native               |
| JS            | JavaScript                 |
| ES6           | ECMAScript 6               |
| UI            | User Interface             |
| JSX           | **J**avaScript **S**yntax e**X**tension|

#### O que é o React-Native:question: 

o **RN** é uma biblioteca baseada no já conhecido [React](https://reactjs.org/), e permite que você desenvolva aplicativos para as plataformas **Android** e **IOS** utilizando apenas **JavaScript**.

Para desenvolvedores com conhecimento em desenvolvimento web, (HTML, CSS, JS) a curva de aprendizado é bem pequena. Se você está familiarizado com ES6 vai ter menos dificuldade caso não esteja dê uma olhadinha nesse curso gratuito da [RocketSeat](https://rocketseat.com.br/starter/curso-gratuito-javascript-es6), lá você também vai encontrar um [curso de RN gratuito](https://rocketseat.com.br/starter/curso-gratuito-react-native) que é muito bom.

#### JSX

È uma sintaxe parecida com XML que permite que você escreva os componentes da UI. É possível fazer uma correlação entre alguns elementos do JSX com tags do HTML

Exemplo:
| HTML          | JSX           |
| --------------|:-------------:|
| div           | View          |
| p             | Text          |
| img           | Image         |

para saber mais sobre JSX acesse a [documentação oficial ](https://reactjs.org/docs/introducing-jsx.html)

#### Componentes 
No RN tudo é componente e isso permite um reuso muito grande dentro da aplicação. Os componentes podem ser de dois tipos **Stateful** e **Stateless** uma explicação sobre cada tipo fica para um próximo post, mas uma explicação rápida é que um gerencia o próprio estado e outro é estático.

Exemplo:

```js
  import React,{ Component } from 'react';
  import { View, Text } from 'react-native';

  export default class MyComponent extends Component{
    render(){
      return (
        <View>
          <Text>Hello React-Native</Text>
        </View>
      );
    }
  }
```

#### State
Como a própria [documentação](https://facebook.github.io/react-native/docs/state) diz é um tipo de dado que controla o componente. O state é mútavel e cada componente pode ter o seu próprio estado.

Exemplo:
```js
  import React,{ Component } from 'react';
  import { View, Text } from 'react-native';

  export default class MyComponent extends Component{

    state = {
      name: 'My-Name'
    }

    render(){
      return (
        <View>
          <Text>Hello {this.state.name}</Text>
        </View>
      );
    }
  }
```
Como visto no exemplo para acessar um dado do state você utiliza a sintaxe:
```js 
this.state.name
```

para alterar o valor do seu state, faça dessa forma

```js 
this.setState({name: 'novo valor'});
```

É possível alterar o state de um componente a partir de outro? sim, é possível mais não é indicado, se você deseja ter um state que possa ser acessado por toda a aplicação você deve utilizar **Redux**, **MobX** ou um similar.

### Props
O Props é outro tipo de dado com o qual você pode controlar o componente, mas diferente do state o prop é definido por um componente pai e passado para um filho, o filho não pode alterar diretamente o valor do props.

Exemplo:
```js
  import React,{ Component } from 'react';
  import {
    View,
    Text,
    TouchableOpacity,
    TextInput
  } from 'react-native';

  export default class MyComponent extends Component{

    state = {
      name: ''
    }

    render(){
      return (
        <View>
          <TextInput
            placeholder="Informe seu nome!"
            value={this.state.name}
            onChangeText={(text) => {
              this.setState(name: text);
            }}
          />
          {/* componente filho */}
          <Button
            name={this.state.name} {/*props enviada ao filho*/}
          />
        </View>
      );
    }
  }

  
  const Button = (name) => (
    <TouchableOpacity
      onPress={() => alert(`Olá ${name}`)}
    >
      <Text>Clique aqui!</Text>
    </TouchableOpacity>
  );
```

#### Conclusão

Bom a partir do que foi apresentado neste texto você já pode prosseguir nos seus estudos sobre o React-Native, aconselho que você leia a [documentação oficial](https://facebook.github.io/react-native/) e pratique bastante, pois isso é só a ponta do iceberg :laughing:. Como complemento deste post estarei escrevendo um tutorial onde faremos um app simples usando os conceitos aqui estudados, então até a próxima  :sunglasses:. 
