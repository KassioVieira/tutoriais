---
  title: Primeiro app com React-Native
  author: Kássio Luz
  date: 02/04/2019
---

Primeiro app com React-Native
-

Olá, no post anterior dei uma introdução sobre o que é React-Native, se você ainda não leu [clique aqui]() para ler. Neste post vamos desenvolver um app simples aplicando os conceitos vistos anteriormente.

Vou considerar que você já configurou todo o ambiente para o desenvolvimento com React-Native, se ainda não configurou segue esse [tutorial](https://rocketseat.com.br/assets/files/ambiente-de-desenvolvimento-rn.pdf) e depois volte aqui, estarei esperando :clock8:. 

Com o ambiente configurado e tudo funcionando vamos dar início ao nosso projeto, execute no seu terminal esse comando.

```sh
  $ react-native init helloWorld
```

Após a execução do comando será criado uma pasta com o nome do nosso projeto, abra essa pasta com o seu editor preferido. I :heart: VsCode

#### Estrutura do projeto
O nosso projeto tem  a seguinte estrutura

![estrutura](https://github.com/KassioVieira/tutoriais/blob/master/1.png "estrutura")

As pastas `android` e `ios` contém os códigos referentes a cada plataforma e dentro de `node_modules` ficam nossas depedências que são gerenciadas pelo `package.json`

#### Mão no código
No arquivo `App.js` você encontrará um código de exemplo gerado pelo React-Native, substitua o conteúdo pelo seguinte código.

```js
import React, { Component } from 'react';

import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
} from 'react-native';


export default class Login extends Component {

  render() {
    return (
      <View>
        <Text>Login</Text>
        <TextInput
          placeholder="Usuário"
        />
        <TextInput
          placeholder="Senha"
          secureTextEntry
        />
        <TouchableOpacity>
          <Text>
            Entrar
        </Text>
        </TouchableOpacity>
      </View>
    );
  }
}
```
Aqui nós utilizamos elementos do **JSX** para escrever o nosso layout, para conhecer todos os componentes disponíveis no react-native veja a [documentação](https://facebook.github.io/react-native/docs/components-and-apis#basic-components) e
para ver o resultado abra o terminal na raiz do seu projeto e digite o seguinte comando

```js
  $ react-native run-android //ou run-ios
```
Se tudo correu bem você deve ter este resultado.
![resultado1](https://github.com/KassioVieira/tutoriais/blob/master/3.png "resultado1")
nada bonito não é mesmo :sweat_smile: ?

Então vamos deixar mais agrádavel, para isso vamos utilizar o componente `StyleSheet`, importe ele em react-native

```js
import {
...
StyleSheet
} from 'react-native';
```

e modifique o arquivo `App.js` para seguinte.

```js
import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
  Alert
  StyleSheet
} from 'react-native';


export default class Login extends Component {

  render() {
    return (
     <View style={styles.container}>
        <Text style={styles.title}>Login</Text>
        <TextInput
          style={styles.input}
          placeholder="Usuário"
        />
        <TextInput
          style={styles.input}
          placeholder="Senha"
          secureTextEntry
        />
        <TouchableOpacity
          style={styles.button}>
          <Text style={styles.textBtn}>
            Entrar
          </Text>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#E1E2E1',
  },

  title: {
    marginBottom: 80,
    color: 'black',
    fontSize: 25,
    fontWeight: 'bold'
  },

  input: {
    margin: 10,
    width: 300,
    height: 60,
    borderWidth: 1,
    backgroundColor: 'white',
    borderColor: 'white',
    borderRadius: 3.17
  },

  button: {
    marginTop: 10,
    width: 300,
    height: 60,
    backgroundColor: '#00756c',
    justifyContent: 'center',
    alignItems: 'center',
    borderRadius: 3.17
  },

  textBtn: {
    color: 'white',
    fontSize: 16
  }
})
```
Como resultado teremos isto.
![resultado4](https://github.com/KassioVieira/tutoriais/blob/master/4.png "resultado4")

Agora sim, ficou bonitão :laughing:

Como você pode ver, podemos escrever o estilo do nosso componente com uma sintaxe muito próxima do CSS.

:exclamation: Alerta de Spoiler :exclamation:

É possível utilizar CSS com o [Styled Components](https://www.styled-components.com/), mas isso é assunto para outro post.

Com isso já temos o layout do nosso app, mas ao clicarmos no botão de login nada acontece, então vamos dar vida ao nosso app.

vamos utilizar o **State** para receber o usuário e a senha e depois criaremos uma função para validar as credenciais.

Adicione o seguinte código ao nosso componente.

```js

  ...

export default class Login extends Component {
 
 state = {
    user: '',
    password: '',
  }

  render() {
    ...
  }
}
```

Feito isso é necessário preencher o estado com o que for informado pelo usuário no `TextInput`, para isso usaremos a propriedade `onChangeText`, nosso código ficará assim.

```js


  ...

export default class Login extends Component {
 
 state = {
    user: '',
    password: '',
  }

  render() {
    ...
     <TextInput
        value={this.state.user}
        style={styles.input}
        placeholder="Usuário"
        onChangeText={(user) => {
          this.setState({ user })
        }}
      />
      <TextInput
        value={this.state.password}
        style={styles.input}
        placeholder="Senha"
        secureTextEntry
        onChangeText={(password) => {
          this.setState({ password })
        }}
      />
    ...
  }
  ...
```

Com isso o state vai receber o que for digitado no `TextInput`, agora vamos criar uma função que vai verificar se a credencial é válida. Claro que vamos fazer uma verificação simples, mas aqui você poderia enviar os dados para uma API e receber o resultado.


```js

...

export default class Login extends Component {

  state = {
    user: '',
    password: '',
  }

  checkLogin = () => {
    if (this.state.user === 'tutorial' && this.state.password === '1234') {
      alert('Usuário logado');
    } else {
      alert('Erro ao realizar login');
    }
  }

  render() {
    return (
          ...
            <TouchableOpacity
              onPress={this.checkLogin}
              style={styles.button}>
              <Text style={styles.textBtn}>
                Entrar
            </Text>
            </TouchableOpacity>
          ...
        );
  }
}
...

```
Note que usamos a propriedade `onPress` do `TouchableOpacity` assim sempre que o usuário clicar no botão nossa função que valida as credenciais será chamada.

:confetti_ball: Comemore o seu primeiro app está pronto :tada: 

#### Conclusão
Bom, com isso nós temos o nosso primeiro app :sunglasses:, rsrs é apenas uma screen simples, mas é o primeiro passo para chegar muito longe e dominar o mundo :earth_americas:.

