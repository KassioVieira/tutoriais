---
title: Primeiro app com React-Native
author: Kássio Luz
date: 02/04/2019
---

## Styled Components com React-Native

Olá pessoal, bom ultimamente comecei a utilizar a biblioteca [`styled-components`](https://www.styled-components.com/) e estou gostando muito de todo o poder que ela nos dar na criação dos nossos componentes. Então vamos fazer um pequeno projeto utilizando essa lib.

#### O que é o Styled Components :question:

O styled components é uma biblioteca que permite que a gente escreva CSS dentro do JavaScript,pode parecer meio estranho, mas isto vai ajudar a você a componentizar sua aplicação, e claro você já deve conhecer a sintaxe do CSS, então a sua curva de aprendizado vai ser baixa.

#### Hora de codificar

Bom neste artigo vou aproveitar o código que fizemos no post anterior, se ainda não leu [clique aqui](https://medium.com/@kassio.vieira7/primeiro-app-com-react-native-5b2096c8ac26) sem medo de ser feliz.

Agora vamos instalar essa biblioteca no nosso projeto.

```sh
$ npm i styled-components
```

Com isso vamos criar nosso primeiro component, para isso crie a seguinte estrutura na raiz do seu projeto `src/components/Button` e dentro dela adicione os arquivos `Button.js` e `styles.js`.

Abra o arquivo `styles,js` e adicione o seguinte código.

```js
import styled from "styled-components/native";

export const WrapButton = styled.TouchableOpacity`
  margin-top: 10;
  width: 300;
  height: 60;
  backgroundcolor: ${props => props.background};
  justify-content: center;
  align-items: center;
  border-radius: 3.17;
`;

export const TextButton = styled.Text`
  color: ${props => props.color};
  font-size: 18;
`;
```

#### Entendo o código

O `WrapButton` é um component assim como `TextButton`. Observando a forma como o componente foi criado, podemos notar que após o sinal de igual temos `styled.View` e `styled.Text` isso é usado para definir o componente que você irá estilizar isso é importante pois algumas propriedades dependem do componente que você está usando.

Também é importante notar o uso de acentos graves **``** isso é o [Template String](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/template_strings) uma feature do javascript.

Por fim também temos `props`no styled-component assim o nosso botão terá um background, texto e cor que pode ser passada dinâmicamente através da `props`. Na [documentação](https://www.styled-components.com/docs/basics#adapting-based-on-props) você encontra vários exemplos de como utilizar o `props` para adaptar o componente, vale a pena a leitura.

Bom com isso podemos partir para o uso do nosso componente, então adicione o seguinte código no `Button.js`

```js
import React from "react";

import { WrapButton, TextButton } from "./styles";

const Button = ({ text, background, color }) => (
  <WrapButton background={background}>
    <TextButton color={color}>{text}</TextButton>
  </WrapButton>
);

export default Button;
```

No arquivo `App.js` faremos uso do nosso `Button`, para isso importe o nosso componente.

```js
...
  import Button from "./src/components/Button";
...
```

e substitua o seguinte trecho

```js
...
  <TouchableOpacity
    style={styles.button}>
    <Text style={styles.textBtn}>
      Entrar
    </Text>
  </TouchableOpacity>
...
```

por

```js
...
  <Button
    background="#00756c"
    color="#FFFFFF"
    text="Login"
  />
  ...
```

O resultado é o mesmo do apresentado ao fim do [post](https://medium.com/@kassio.vieira7/primeiro-app-com-react-native-5b2096c8ac26) anterior, mas dessa vez utilizando Styled Components.

![resultado4](https://github.com/KassioVieira/tutoriais/blob/master/4.png "resultado4")

Com isso temos nosso primeiro componente que utiliza essa biblioteca. Para praticar você pode reescrever os demais componentes utilizando o Styled Componentes, também estude a documentação para aprender mais sobre a biblioteca.

#### Conclusão

Neste artigo falei um pouco sobre o que é o Styled Component, e criamos um componente utilizando essa biblioteca, passando por alguns detalhes fundamentais sobre ela, existem mais coisas que você pode explorar dessa lib então bons estudos e até a próxima.
