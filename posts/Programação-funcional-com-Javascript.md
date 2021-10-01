---
title: 'Programação funcional com Javascript'
date: '2021-10-01'
---

# Programação funcional com Javascript

## O que programação funcional?

É um entre outros paradigmas de programação como a programação imperativa e a programação orientada a objetos.

Neste paradigma, como o próprio nome já diz as funções são o centro das atenções! 

Além de ser um paradigma da programação, a programação funcional também é um estilo de codificação. É uma maneira diferente de abordar e resolver problemas utilizando a programação. 

Ainda mais, a programação funcional representa também uma mudança de *mindset* do programador.

## Por que utilizar programação funcional?

Existem algumas vantagens na utilização da programação funcional, desse modo podemos citar algumas como:

- Reduzir o risco de bugs(em comparação a POO)
- Mais seguro
- Menos complicado
- Mais fácil de depurar
- Manutenção mais fácil

Outra motivo bastante pautável para a utilização de programação funcional é comunidade bem estabelecida no assunto, principalmente quando falamos de *Javascript*, uma que a POO em *Javascript* é um tanto quanto diferenciada, o que acaba atrapalhando um pouco aqueles que desejam aprender ou utilizar orientação a objetos usando está incrível e fascinante linguagem de programação. Assim podemos analisar que já existem diversas bibliotecas que podem ajudar na escrita de códigos funcionais no *Javascript*. Desse modo se deseja aprender programação funcional utilizando o *Javascript* você não precisa necessariamente fazer isso sozinho.

## Como usar a programação funcional?

A primeira a coisa a entender, e que pode soar um tanto quanto redundante é que na programação funcional tentamos expressar todo código possível usando função que recebe entradas e retorna saídas. Desse modo novamente comparando com a programação orientada objetos, na programação funcional lidamos com o fluxo dos dados, suas entradas e saídas ao contrário da POO onde temos que nos preocupar com na iteração entre os objetos de diferentes classes.

Este é um exemplo de como não usar a programação funcional, o que você vê aqui é basicamente programação imperativa onde basicamente tudo é cronológico e você trabalha com afirmações do tipo, "Faça isso depois faça aquilo e então aquele outro!".

```jsx
var nome = "Pedro"
var inicioDaFrase = "Ola, "
console.log(inicioDaFrase + nome)
// -> Olá, Pedro
```

Dessa forma uma maneira um tanto quanto funcional de resolver o mesmo problema seria utilizando uma função que recebe o nome da pessoa coo parâmetro e retornando a concatenação de uma saudação inicial e o nome passado com parâmetro da função. depois disso poderíamos dar saudação a qualquer pessoa em qualquer momento pois sabemos que escrevemos uma função para isso:

```jsx
function bemVindo(nome) {
    return `Ola, ${nome}`
}
bemVindo("pedro")
// -> Olá, Pedro
```

## O que são funções puras?

Funções puras são funções que buscam evitar ou famosos *side-effects* (em português, efeitos colaterais), desse modo no paradigma da programação funcional, devemos usar funções puras!

Funções puras são funções que recebem um valor como entrada computam o valor e retornam sua saída, nada além disso.

Caso uma funções faça algo além de receber, computar e retornar dados ela não poderá ser categorizada como uma função pura.

### Exemplo de função "impura":

```jsx
var nome = "Pedro"
function bemVindo) {
    console.log(`Ola, ${nome}`)
}
```

Explicando de maneira simples a função, acima não pode ser considerada uma função pura pois não recebe entradas, não retorna saídas, utiliza-se de dados externos e executa efeitos colaterais.

### Exemplo de função "pura"

```jsx
function bemVindo(nome) {
    return `Ola, ${nome}`
}
```

Agora sim, essa função é uma função pura, uma vez que apenas se importa com receber um dado específico e retornar um resultado.

## O que são funções de order suprema?

*High order function*, ou funções de ordem suprema são funções que estão categorizadas um nivel acima da hierarquia de funções uma vez que estas, e apenas  estas, podem receber e(ou) retornar outras funções. Quando falamos que na programação funcional tudo deve ser funções as funções de ordem suprema ajudam muito pôs nos permitem encapsular funções dentro de outra funções e assim construir a lógica da nossa aplicação a fim de revolucionar o problema da melhor e mais eficiente maneira possível.

Um exemplo da utilização de funções de ordem suprema na programação funcional seria o códido a seguinte:

```jsx
function criarAdjetivo(adjetivo) {
    return function (string) {
        return `${string} ${adjetivo}`
    }
}

var deixaLegal = criarAdjetivo("legal")
deixaLegal("Programação")
// -> Programação legal
```

Aqui basicamente estamos criando a função para criar um adjetivo que recebe como parâmetro um adjetivo e retorna uma função que recebe uma *string* e retorna a concatenação da *string* com o adjetivo. Dessa forma temos uma função que chama outra função.

## Use função de ordem suprema pré-prontas

A ideia é que paremos de usar funções como o `while`, `for in`, `for of` e `do while` para iterar sobre elemento e usemos funções como `map`, `reduce` e `filter` para não só percorrer listas mas executar determinadas funções em cada um dos elementos.

Um exemplo rápido da utilização dessa funções seria da seguinte forma:

- Imaginamos que tenhamos uma lista com vários ingredientes e queiramos fazer um sanduiche com eles.
- Estes ingredientes estão despreparados, acabamos de pega-los de uma geladeira por exemplo.
- Então percebemos que precisamos que todos eles sejam fatiados.
- Para isso poderíamos usar o método de listas `map` que executa uma determinada função para cada item em uma lista.
- No nosso caso executará a função de fatiar para cada ingrediente de nosso sanduiche.
- Depois disso percebemos que agora a mesma lista contém apenas elementos fatiados e já finalizados.
- Depois disso poderiamos utilizar a função reduce para montar nosso sanduiche de fato.

## Utilize dados imutáveis

Use dados imutáveis, isso é utilize dados que tenham o mesmo valor em toda a execução do código para evitar erros e auxiliar na depuração de código já que caso ficarmos alterando o valor de uma determinada variável podemos ter um erro nela e não entender qual o valor dela em determinada execução do código, o que acaba dificultando o processo de debug por exemplo.

Sendo assim utilize o `const` sempre que for possível e não altere valores, mas sim crie novos dados baseados nos antigos:

### Exemplo de variavél muável e código não funcional:

```jsx
var salas = ["f1", "f2", "f4"]
console.log(salas);
// -> ["f1", "f2", "f4"]
salas[2] = "f3"
console.log(salas);
// -> ["f1", "f2", "f3"]
```

Nesse código alteramos o valor da variável salas em plena a execução do código o que pode causas problemas.

### Exemplo de código funcional, utiizando constantes?

```jsx
const salas = ["f1", "f2", "f4"]
console.log(salas)
// -> ["f1", "f2", "f4"]
const novasSalas = salas.map(sata => sala === "f4" ? "f3" : sala)
console.log(salas)
// -> ["f1", "f2", "f4"]
console.log(novasSalas)
// -> ["f1", "f2", "f3"]
```

Nesse código utilizamos a função de ordem suprema `map` para alterar o valor dar sala esperada e retornar uma  nova lista com o valor da sala, desse modo utilizamos a programação funcional!

## Como aumentar a eficiência usando a imutabilidade

Temos um lógico problema de eficiência e aumento de complexidade quando paramos de reusar os dados já existentes e ficamos toda hora criando novas estruturas de dados para modificar qualquer coisa. Dessa forma podemos ser seletivos e usar a mutabilidade quando o nível de complexidade e eficiência computacional começar a ser prejudicial para o nosso código e desta forma ferir um poucos os princípios da programação funcional.

Ou podemos utilizar conceitos como *"Persistent data structures"* para resolver o problema. Esse conceito em questão é um conceito um tanto quanto complexo e requer conhecimento de estrutura de dados para entende-lo e aplica-lo. Sendo assim não vou entrar em méritos de explica-lo aqui no, entanto caso julgue necessário pode procurar saber mais sobre ele por conta própria para ajudar você a resolver esse tipo de problema de complexidade aferido devido a programação funcional.

No entanto saiba que existem bibliotecas (Mori, Immutable.js) que podem ajudar você com isso implementando estruturas de dados persistentes em seus códigos *Javascript* de maneira mais fácil.

# Possíveis duvidas?

- Programação funcional é melhor que a programação orientada a objetos ou a programação imperativa?
    
    Não! Mas talvez sim ! A questão é que podem ser melhores ou piores para alguns casos, e também não há motivos para não usá-los juntos. E a mesma história das brigas para decidir qual é a melhor linguagem de programação. E a resposta para os dois casos é a mesma: "A melhor linguagem/paradigma é aquele que resolve o seu problema dada as devidas condições!"