---
layout: post
title: "Desenvolvendo um app mobile com Ionic 3, Parte 2 - Consumindo dados de uma api"
author: "Hallessandro D´villa"
categories: journal
tags: [ionic,app, mobile, multiplataforma]
---

Olá terráqueos, nesse post vamos avançar um pouco mais a app criada no primeiro [post](https://hallessandro.github.io/journal/first-app-ionic.html) sobre Ionic 3.  Se lá no primeiro post a gente apenas criou a app, neste vamos ver como consumir uma api online e como exibir esses dados na tela em forma de lista. 


Para começar acesse o arquivo home.html, que fica localizado em: 

> src -> pages -> home -> home.html

Dentro desse arquivo, você vai encontrar um código bem parecido com o apresentado abaixo, ele é o responsável por criar aquela tela visualizada quando você executou o comando "ionic serve --lab". 

```html
<ion-header>
  <ion-navbar>
    <ion-title>
      Ionic Blank
    </ion-title>
  </ion-navbar>
</ion-header>

<ion-content padding>
  The world is your oyster.
  <p>
    If you get lost, the <a href="http://ionicframework.com/docs/v2">docs</a> will be your guide.
  </p>
</ion-content>
```

Repare que o código é dividido entre duas tags principais, o ion-header e o ion-content. O primeiro é responsável por toda a parte de cabeçalho da tela, enquanto que o segundo é o responsável pelo conteúdo em si. Fique a vontade para substituir o valor presente em ion-title por um valor que tenha alguma relação melhor com a sua app. 

Remova tudo que está dentro do bloco ion-content, pois nós vamos substituir esse conteúdo por algo mais interessante. 

Quando estamos trabalhando com Ionic, a melhor forma de exibir os dados em uma tela em forma de lista é utilizando o elemento ion-list, onde por exemplo, para criar uma lista com três elementos na tela, poderia se fazer algo como: 

```html
<ion-list>
  <ion-item>Item 1</ion-item>
  <ion-item>Item 2</ion-item>
  <ion-item>Item 3</ion-item>
</ion-list>
```

Faça o teste, adicione o código acima entre às tags do ion-content do seu arquivo home.html e então execute o ionic serve --lab. 

E ai? Se você fez o teste, viu que ao executar é exibido uma pequena lista com três elementos na tela, até ai tudo ok certo? Mas se você reparou bem, nossa lista é estática e no final das contas não tem muita utilidade, afinal o que vou fazer com uma lista de itens sem graça? 

Pensando nisso, é hora de dar um upgrade na nossa app, vamos consumir uma api online para obter alguns dados, e a partir dai vamos exibir esses dados na tela. A ideia aqui é começar exibindo os dados da forma mais simple e depois ir melhorando gradativamente essa exibição. 

A partir da versão 4.3 do Angular, trabalhar com requisições http ficou mais fácil, graças ao HttpClient... 

**Referências:**

[Documentação Ionic - List](https://ionicframework.com/docs/api/components/list/List/)
[HttpClient](https://angular.io/guide/http)