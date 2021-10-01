---
title: 'Tratamento de erro no Javascript'
date: '2021-10-01'
---

# Tratamento de erros no Javascript

## O que são erros?

Erros são simplesmente problemas ou algo que não aconteceu como desejávamos.

## Para que servem os erros?

Os erros tem a função de interromper um programa em execução, já que algo deu errado e o computador não tem mais a capacidade de seguir a execução do código, a não ser que o erro seja tratado corretamente.

## Por que se preocupar com erros?

- Manutenção do código
- Melhorar/facilitar o processo de *debugging*
- Resiliência → Fazer com o que o seu código se adapte as situações mais adversas. "Se o objetivo do erro é interromper a execução do código, o tratamento de erro é fazer com que o código continue sendo executado mesmo que algo não esperado aconteça."

## Quando os erros acontecem?

- Quando tentamos invocar uma função que não existe
- Quando escrevemos um código com a sintaxe errada.
- Quando passamos um parâmetro errado a uma função

## Quais são os prováveis cenários de erros?

- Input de dados sem tratamento são uma grande possibilidade de erro já que uma função pode esperar um valor de entrada de uma forma e como o input não foi validade devidamente a função recebe um dado sem sentido o que acaba ocasionando um erro e posteriormente finalizando a execução do código.
- Usuários sem internet são um grande problemas pois com trabalhamos com a WEB basicamente tudo precisa acesso a internet para funcionar corretamente no entanto não existem desculpas como esta no mundo dos desenvolvedores, assim  é necessário tratar problemas como este de forma a manter ao máximo a funcionalidade da aplicação sem danificar/prejudicar a regra de negócio.
- Serviços de terceiros, necessários para o funcionamento da aplicação, não disponíveis(ou com mal funcionamento) podem causar gravíssimos problemas, caso o tratamento de erros não seja feito ou seja realizado de forma errônea.
- Utilizar funcionalidades do navegador, telefones, notebooks, TVs que não existem também são erros muito comuns já que trabalhamos com uma variedade imensa de dispositivos e eles podem ser infinitamente diferentes uns dos outros. Caso não pensemos nestas possibilidades, nossas aplicações podem funcionar de maneira indevida ou até mesmo não funcionar, prejudicando assim a experiência do usuário e as regras de negócio da aplicação.

## Por que criar erros?

- Para sermos mais específicos conquanto o que está acontecendo, desta forma agindo de uma maneira mais eficiente.

## Como criar erros?

```jsx
const meuErro = new Error("Esse é o meu erro!")

console.log(meuErro)
```

Neste trecho de código basicamente criamos um erro utilizando a propriedade padrão para erros no Javascript e após isso imprimos no console o erro. Apesar de correta, a utilização do objeto Error ainda é muito generalista, já que o Javascipt da suporte nativamente para que possamos utilizar erros mais espécificos como os tipos a seguir:

- EvalError ⇒ Cria uma instância representando um erro que ocorre na função global. eval().
- InternalError ⇒ Cria uma instância representando um erro que ocorre quando um erro interno na engine do JavaScript é lançado. Ex: "too much recursion", em português "com muita recursão".
- RangeError ⇒ Cria uma instância representando um erro que ocorre quando um valor ou parâmetro numérico está fora de seus limites válidos.
- ReferenceError ⇒ Cria uma instância representando um erro que ocorre ao de-referenciar uma referência inválida. Acontece geralmente como no caso supracitado de tentar invocar uma função que ainda não foi definida.
- SyntaxError ⇒ Cria uma instância representando um erro que ocorre ao fazer o parse do código em eval(). Erros de sintaze ocorrem quando o código executado está com uma sintaxe não legivél pelos interpretadores do Javascript.
- TypeError ⇒ Cria uma instância representando um erro que ocorre quando uma variável ou parâmetro não é de um tipo válido.
- URIError ⇒ Cria uma instância representando um erro que ocorre quando são passados parâmetros inválidos para encodeURI() ou decodeURI().

## Como verificar o tipo de erro?

```jsx
const meuErro = new Error("Esse é o meu erro!")

console.log( meuErro instanceof Error )
```

No bloco de código acima verificamos se o erro que criamos é uma instancia da classe Error, neste caso o código ao ser executado nos retornaria true como resposta já que a constante meuErro se trata de uma instancia da classe Erro. No entanto caso tentassemos executar esse código testando se meuErro é uma instancia da classe SyntaxError obteriamos como resposta o dado booleano false.

## Como encontrar a causa do erro?

Encontrar a causa do erro para que ai de fato possamos corrigi-lo é extremamente necessário dessa forma veremos a propiedade stack que é acessivél em todos os objetos de erro criados apertir da classe Error ou das classes que se extende a ela como a SyntaxError e TypeError já citadas anteriormente. Mas o que a propiedade stack nos diz? ela basicamente nos informa o trajet/caminho de excução até que se chege no erro em quetão. Exemplo:

```jsx
function criaErro() {
    const meuErro = new Error("Este é o meu erro")
    console.log(meuErro.stack)
}

function testeStack() {
    console.log("Está é a função testeStack que chama a função criaErro")
    criaErro()
}

testeStack()
```

No código acima criamos a função testeStack que chama a função criaErro que de fato cria um erro e imprime em nosso console a propidade stack da instância da classe erro. Desta forma ao executar este códido receberemos como resposta em nosso conole o seguinte:

```jsx
Está é a função testeStack que chama a função criaErro
Error: Este é o meu erro
    at criaErro (C:\Users\Azeplast2\Desktop\Desafio de Programação\app.js:2:21)
    at testeStack (C:\Users\Azeplast2\Desktop\Desafio de Programação\app.js:8:5)
```

Então agora entemos que além de retornar a mensagem de nosso erro o atributo stack nos informou que o erro foi encontrado na execução da função criaErro que está dentro da função testeStack.

## Como lançar um erro e interrepomper a execução do código?

A resposta da pergunta acima é bastante simples e se trata de se utilizar da palavra reservada **throw** do javascript. Sendo assim vamos ver a definição da MDN - Mozilla Developer Network da declaração throw:

> "A declaração throw lança uma exceção definida pelo usuário. A execução da função atual vai parar (as instruções após o throw não serão executadas), e o controle será passado para o primeiro bloco catch na pilha de chamadas. Se nenhum bloco catch existe entre as funções "chamadoras", o programa vai terminar."
> 

Agora que temos a definição da declaração throw, vamos ver ná prática como ela funciona, utilizando também um exemplo da documentação da MDN, traduzido para português:

```jsx
function getMonthName(mo) {
   mo = mo-1; // Ajusta o número do mês para index de array (1 = Jan, 12 = Dec)
   var months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul",
      "Aug", "Sep", "Oct", "Nov", "Dec"];
   if (months[mo] !== undefined) {
      return months[mo];
   } else {
      throw new Error("Numero do mês indefinido");
   }
}
var myMonth = 15; // 15 é um numero maior que o esperado pela função a ser chamada
monthName = getMonthName(myMonth);

```

## Como tratar os erros?

Agora que ja entemos o que são erros? Para quq eles servem? Por que se preucupar com eles? Quando eles acontecem? Quais são os principais cenérios onde eles aparecem? Por que criá-los? Como criá-los? Como verificar seu tipo? Como encontrar sua causa? E como lança-los? Vamos começar com a parte extremamente necessária por todos os motivos que já citamos aqui! Como tratá-los?

### Try / Catch / Finnaly

Quando falamos de tratamentos de erros, independente da linguagem de programação fica muito dificil não falar do famoso try e catch ou de alguma função de nome parecido que realize praticamente a mesma coisa. Caso você ainda não conheceça esta função funciona da seguinte forma:

```jsx
try { //Tenta executar o bloco de código e caso não consega chama a afunção catch passando como atributo o erro gerado
    
} catch (error) { //Recebe um erro e executa um bloco de códido para tratá-lo
    
} finally {//Ao final da execução do try ou do catch a função é chamada e seu bloco de código é excutado

}
```

Try / Catch são utilizados em praticamente todo código onde executamos um tratamento de erros bem feito, desta forma vamos dar um exemplo da boa utilização destas função, simulando um caso em que o usuário ficou sem internet:

Imanginamos que estamos criando um sistema que necessita constantemente fazer requisições a uma API externa para obter e enviar dados entre o cliente e o nosso servidor, se por algum motivos o nosso cliente ficar sem internet e a nossa aplicação tentar executar uma dessas requisições, vai receber um erro chamado de time-out  que em porugês significa algo como "Tempo expirado" ou seja, o navegador está no dizendo que tentou realizar a solicitação por muito tempo, no entanto não obteu exito, desta forma o usuário receberia um erro tosco na tela e se não tiver conhecimento na area ou na lingua inglesa vai ficar perdido e confuso. Assim, o que seria o ideal a fazer nestes casos? Existem diversas formas de tratar erros como estes, mas o que eu faria seria algo como:

```jsx
try {
	// Função que faz a requisição a API

} catch (error) {
	// Se o erro for um time-out
  // Testo a conexão com a internet do cliente
	// Se a conexão não estiver funcionando
	// Imprimo uma mensgaem ao usuário dizendo para que ele perceba que está sem interet
	// Enquanto isso testo a cada 3 segundo se a conexão pode ser realizadas
	// Caso a internet volte a funcionar
	// Invoco novamente a função que faz a requisição a API
}
```
