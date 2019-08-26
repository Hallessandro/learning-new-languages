---
layout: post
title: "#4 - Introdução ao Meteor - Parte 2"
author: "Hallessandro D´villa"
categories: programming
tags: [meteor,javascript, node, meteorjs]
image: coverPosts/meteor2.png
header-img: "coverPosts/meteor2.png"
---

Olá terráqueos, no primeiro post sobre  Meteor, que você pode encontrar [aqui](https://hallessandro.github.io/programmi/introducao-meteor.html), vimos como construir uma aplicação Meteor de cadastro de livros. Atualmente a aplicação permite o cadastro de novos livros além de exibir os livros já existente. Nesse post vamos aprimorar essa aplicação, permitindo agora a edição e remoção dos livros presentes na lista. 

> Talvez você tenha notado que tanto neste post quanto na primeira parte, alguns códigos demonstrados são imagens, enquanto que outros são em blocos de código mesmo, isso ocorre haja vista que o Markdown não renderiza os códigos que estão entre chaves, como por exemplo {{>nome}}, por esse motivo todos os blocos de código que em alguma parte utilizem código entre chaves, estão sendo exibidos em forma de imagem. 

Para começar, vamos atualizar o template de lista, adicionando dois botões, um para editar e outro para remover. Além disso vamos atualizar a forma como os dados são apresentados de uma lista para uma tabela, apenas para deixar as coisas um pouco mais organizadas. 

![Código do template de lista.html](../assets/img/Post2Meteor/code1.png) 

Se você se lembra do primeiro post, para adicionar um novo livro a gente tratou o evento de submit do form em novo.js, fazendo com que ele resultasse na adição do novo livro. Vamos realizar esse mesmo tipo de tratamento para os nossos novos botões, começando pelo de remover, para isso altere o arquivo lista.js deixando o desta forma: 

```javascript
Template.lista.helpers({
	livros: function () {
		return Livros.find({});
	}
});
Template.lista.events({
    "click button" : function (e, template) {
            let livro = this; 
            Livros.remove({_id: livro._id});
    }
});
```

Teste a execução do código acima e veja o resultado, clique em ambos os botões. Se tudo ocorreu como deveria você deve ter notado que existe um comportamento nada desejado com nossos botões, tanto o de editar quanto o de remover estão removendo o registro, e definitivamente não é isso que desejamos. Isso ocorre pois estamos capturando o evento de "click button" ou seja, clique do botão, mas em nenhum momento falamos para o Meteor qual o botão, assim quando qualquer botão existente na página for clicado, ele vai disparar o evento. 

Para resolver isso vamos adicionar uma classe em cada um dos nossos botões: 

```html
	<button class="editar">Editar</button>
	<button class="remover">Remover</button>
```

Agora em lista.js ao invés de capturar apenas o evento de clique vamos capturar o evento de clique para o botão que possui a classe remover. Isso vai resolver o problema limitando que a ação só ocorra quando o botão possuir a classe correta.  

```javascript
Template.lista.events({
    "click button .remover" : function (e, template) {
            let livro = this; 
            Livros.remove({_id: livro._id});
    }
});
```
Agora vamos implementar o evento que vai responder ao botão de editar, para isso em lista.js adicione o código abaixo: 

```javascript
//Código anterior omitido 
"click button .editar" : function (e, template){
    let livro = this; 
    let resultado = Livros.findOne({ _id: livro._id;});
    if(resultado){
        let inputNome = $("#livro");
        inputNome.val(resultado.nome);
        let inputIdLivro = $("#id"); //Esse vai ser um input hidden
        inputIdLivro.val(livro._id);
    }
}
```
>O findOne() utilizado, retorna apenas um documento que satisfaça a condição passada na consulta, por mais que haja outros resultados ele vai retornar apenas o primeiro, diferente do find() que pode retornar vários resultados, dependendo das condições passadas na consulta. 

Agora quando clicado no botão de editar, o input que possui o nome do livro vai ser preenchido com o valor do livro que estamos editando, porém talvez você tenha reparado que estamos passando o _id do livro para um input no template, porém esse campo não existe, vamos resolver isso agora. 

```html
<template name="novo">
    <form>
        <label for="livro">Livro</label>
        <input type="text" id="livro" name="livro">
        <input type="submit" value="Cadastrar">

        <input type="hidden" name="id" id="id">
    </form>
</template>
```
Repare que o input é do tipo hidden, isso pois não queremos que o usuário digite valores para esse campo, ele vai receber algum valor apenas quando clicado no botão de editar. Vamos usar isso no evento que adiciona nosso livro no banco, alterando a forma como ele está implementado atualmente. 

```javascript
Template.novo.events({
    "submit form" : function (e, template) {
            e.preventDefault();
            let input = $("#livro");
            let nome = input.val();
            let inputId = $("#id");
            if(inputId.val()){
                    Livros.update({_id: inputId.val()}, {
                            $set: {nome: nome}
                    });
            }else {
                    Livros.insert({nome: nome});
            }
            input.val("");
    }
});
```
Agora nossa função não vai ser responsável apenas por adicionar registros, mas também por atualizar os registros já existentes, e para que isso funcione ela precisa identificar o que deve fazer quando for acionada, por esse motivo o input do tipo hidden foi adicionado no template, assim sempre que esse campo possuir um valor, um update será executado ao invés do insert. 

Com isso chegamos ao fim deste post, no próximo post vamos ver como melhorar nossa aplicação adicionando Bootstrap e um sistema de login, então até a próxima. 

**Referências:**

1. [Site oficial](https://www.meteor.com/)
2. [Build A Meteor.js App In 45 Minutes](https://www.youtube.com/watch?v=9494-2E4riQ)
3. [What Is Meteor?](https://www.youtube.com/watch?v=eOi3F6Kbl7E)
4. [Why use meteor](https://www.youtube.com/watch?v=6_8B3mi1m18)
5. [Meteor: Crie single page applications com JavaScript](https://www.alura.com.br/curso-online-meteorjs)
6. [Criando aplicações web real-time com JavaScript](https://www.casadocodigo.com.br/products/livro-meteor)
7. [db.collection.findOne()](https://docs.mongodb.com/manual/reference/method/db.collection.findOne/)
8. [db.collection.update()](https://docs.mongodb.com/manual/reference/method/db.collection.update/)