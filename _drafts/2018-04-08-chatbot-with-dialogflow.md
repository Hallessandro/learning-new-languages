---
layout: post
title: "Criando um chatBot com DialogFlow"
author: "Hallessandro D´villa"
categories: journal
tags: [chatbot,dialogflow]
---

Olá terráqueos, nesse post vamos aprender a criar um chatbot capaz de detalhar 


Tópicos para abordar: 

1. O que são chatbos e pq isso está tão em alta?
2. Tópicos que anotei no caderno
3. No final, um tópico sobre como vamos evoluir mais esse chatbot, falar sobre add um backend servindo conteudo. 

Que informações ele deve dar:
--Nome do livro
--Autor
--Ano
--Resumo

Como nessa parte vai ser tudo estático, posso usar os livros abaixo como exemplo:
1- O Hobbit ou só Hobbit (Cadastrar variação)
2- Misery - Louca Obsessão, ou apensa Misery, ou só Louca obsessão (Cadastrar as variações de escrita para esse livro)
3 - Eragon
4 - O pistoleiro 
5 - Mar de monstros 


Tutorial 


Logo após realizar o login você será apresentado a uma tela como a mostrada abaixo:

Imagem

Escolha a opção CREATE AGENT, na janela seguinte você deve informar o nome do seu agente, e definir qual o idioma padrão do bot. É importante que você escolha o PT-BR caso deseje se comuncar em português com seu bot. 

Imagem

Depois de criado, agora é hora de criar nossa primeira intent, de a ela o nome que desejar, no meu caso estou chamando de book-intent. Você vai ver que nessa página há alguns menus como Contexts, Events, Responses e etc. Nesse momento vamos utilizar dois desses, o Training Phrases e o Responses, o primeiro serve para que possamos cadastrar algumas variações de perguntas que o usuário possa fazer ao nosso bot.

Já o Response é onde você deve informar uma ou mais respostas que o bot deve apresentar, quando receber um questionamento do usuário. 

Para esse exemplo, cadastrei algumas variações de perguntas sobre informações referentes ao livro O Hobbit, como pode ser visto na imagem abaixo: 

Imagem

Já para resposta, cadastrei apenas uma, com um pequeno resumo sobre o livro: 

Imagem

Depois cadastrar as variãções de frases para treino e de cadastrar pelo menos uma resposta, clique no botão SAVE, que fica no topo da página, ao lado do nome da intent. 

Agora é hora de testar o nosso progresso até aqui, para isso, no canto direito da sua janela, há uma pequena janela, como a exibida na imagem abaixo, que é o console de teste. Tente perguntar alguma coisa relacionada ao Hobbit e veja o que é retornado. 

Não teste apenas com frases iguais as que você passou para treino, faça variações dessas frases e veja se o bot é capaz de identificar e responder corretamente.

Se tudo ocorreu como deveria, seu bot foi capaz de identificar e responder corretamente, mesmo com variações de perguntas relacionadas ao Hobbit. Mas e se você perguntar a ele por informações sobre Misery por exemplo? Ele com toda certeza não faz ideia do que seja, e consequentemente não tem como responder corretamente, afinal nunca foi ensinado nada a ele sobre isso. 

