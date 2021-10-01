---
title: 'Funções de callback no Javascript'
date: '2021-10-01'
---

# Funções de callback no Javascript

A tradução literal de callback é basicamente "Chame de volta" ou "Chamada de volta", desse modo podemos pressumir que calback function são funções chamadas de volta ou funções de retorno.

## Como é possivel?

O que permite a utilização desse tipo de funções em nossos códigos Javascript é o conceito da matemática e da ciência da computação chamado de HOF - (High Order Function ou Funções de ordem maior) que basicamente separa as funções de ordem primária das funções de ordem maior pela capacidade de retornar/receber funções como resposta /parâmetro ou não, respectivamente. No entanto, para que isso funcione corretamente, no Javascipt funções em geral são consideradas First-class citzen desse modo são tipos de como quaiser outros, assim podendo ser passadas como parâmetro, atribuidas a contantes, variaveis assim como qualquer outro tipo de dado no Javascript.

```jsx
//Armazenando uma função em uma constante
const soma = (a, b) => {
	return a + b;
}

soma(6, 5) ;

//Recebendo funções como parâmetro
function somaFaz= (a, b, callback){
	soma = a + b;
	callback(soma);
}

somaFaz(6, 94, (result) => console.log(result));

//Retornando função
function retornaFunction (a, b) {
	if(a > b) return retornaFunction(a - 1, b);
	else return console.log("A menor que B!");
}

retornaFunction(5, 2);
```

## Exemplo de funções de callback

```jsx
button.addEventListener('click', () => {
	//ação no click
})
```

## Por que são usadas?

Funções de callback podem ser utilizadas em vários casos, no entanto seu grande poder vem na utilização de funções assíncronas, onde a função precisa aguardar a execução de alguma promessa, para que ai de fato possa ter algum retorno, dessa forma as funções assíncronas podem ajudar muito nessa tarefa! UM exemplo da utilização são as requisições para APIs. Exemplo:

```jsx
axios.get('http://link-api.com/') //Executa requisição assincrona
	.then(function (res) { //quando a requisição for realizada chamara a função de callback
		console.log(res.data) //Fulção de callback printa o resulta da função assinncrona
	}
)
```