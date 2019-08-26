---
layout: post
title: "#6 - Construindo uma API REST com Node js"
author: "Hallessandro D´villa"
categories: programming
tags: [rest, node, javascript, nodejs]
image: coverPosts/nodejs.jpeg
header-img: "coverPosts/nodejs.jpeg"
---
Olá terráqueos, neste post vamos construir uma api rest utilizando Node JS e MongoDB. O projeto vai ser uma api de livros que vai poder ser acessada pelo endereço /livros, sendo capaz de responder aos métodos GET, POST, PUT e DELETE. 

Primeiro de tudo, você precisa ter o Node e o MongoDB instalados, caso ainda não tenha, você pode dar uma conferida nos links abaixo, ambos da DigitalOcean: 

```
[Como Instalar o MongoDB no Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/como-instalar-o-mongodb-no-ubuntu-16-04-pt)
```

```
[Como Instalar o Node.js no Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/como-instalar-o-node-js-no-ubuntu-16-04-pt)
```

Feitas as devidas instações, vamos começar a criar nosso projeto, primeiro crie um diretório com o nome do projeto, no meu caso chamei de livros-api, e dentro dele crie os diretórios models, routes e conf, além do arquivo index.js. 

Agora em um terminal acesse o diretório do projeto e digite npm init, para criar o package.json do projeto. Durante esse processo algumas perguntas vão ser feitas, basta ir respondendo conforme sugerido. 

Agora vamos instalar o express e o babel, o primeiro é que há de melhor para se trabalhar com apis em Node, já o segundo é um módulo que permite a utilização de tudo que há de bom no JavaScript ES6/ES7, pois o Node ainda não da suporte completo para esses caras. 

> $ npm install babel-cli babel-preset-es2015 --save
>
> $ npm install express --save

Para que tudo funcione, precisamos linkar o plugin babel-preset-es2015, para que o babel reconheça códigos ES6, para isso basta adicionar na raiz do projeto o arquivo .babelrc, com o seguinte código: 

```json
{
    "presets" : ["es2015"]
}
```

Agora vamos atualizar o package.json, mais especificamente a parte de scripts, onde vamos adicionar o start, que serve justamente para iniciar nosso projeto, quando o comando **npm start** for executado. 

```json
"scripts": {
	"start": "babel-node index.js"
},
```

Repare no comando, babel-node, esse carinha é utilizado para compilar todo o código ES6/ES7 de forma que o node consiga entender.

Agora em **index.js** vamos criar o primeiro código da api. Esse código vai carregar o express e criar um endpoint GET que vai retornar uma simples mensagem em formato JSON. 

 

```javascript
var express = require('express');
const app = express();

app.get("/", (req, res)=>{
    res.json({status : "Olá terráqueos"});
});
app.listen(3000, () => console.log("Servidor rodando na porta 3000"));
```

Para testar esse código, execute **npm start** no terminal, se tudo der certo, será exibido a mensagem de servidor rodando e você pode acessar **http://localhost:3000/** e ver a mensagem Olá terráqueos em formato JSON. 

Agora vamos implementar o GET /livros que vai retornar uma lista de livros. Por hora não estamos conectados a nenhum banco, então vamos retornar apenas uma lista de itens estáticos. Para isso adicione o código abaixo, logo depois do app.get() criado anteriormente.

```javascript
app.get("/livros", (req, res) => {
    res.json({
        livros : [
            {nome : "O Hobbit"}, 
            {nome : "E não sobrou nenhum"}
        ]
    })
});
```

Para ver se tudo funcionou como deveria, pare o servidor e inicie novamente, se tudo deu certo, você vai ver algo como: 

```json
{"livros":[{"nome":"O Hobbit"},{"nome":"E não sobrou nenhum"}]}
```

Nosso projeto é pequeno, mas pense um pouco, o que aconteceria se você fosse criar 20 ou 30 endpoints? O index.js ficaria enorme e nada organizado. Para resolver isso vamos adicionar o módulo consign ao projeto, que nos permite injetar e carregar dependências de forma simples. 

> npm i consign --save

Com esse módulo instaldo, vamos migrar os códigos dos dois endpoints criados, para dois novos arquivos que serão criados dentro de routes, o indexEndPoint.js e o livrosEndPoint.js. 

O arquivo indexEndPoint.js deve ficar assim: 

```javascript
module.exports = app => {
    app.get("/", (req, res) => {
        res.json({status: "NTask API"});
    });
};
```

Já o livrosEndPoint.js deve ficar assim: 

```javascript
module.exports = app => {
    app.get("/livros", (req, res) => {
        res.json({
            livros : [
                {nome : "O Hobbit"}, 
                {nome : "E não sobrou nenhum"}
            ]
        })
    });
};
```

Agora edite o index.js para que ele possa carregar ambos os endPoints e então iniciar o servidor, para isso faça: 

```javascript
var express = require('express');
var consign = require('consign');
const app = express();


consign()
    .include("routes")
    .into(app);
    
app.listen(3000, () => console.log("Servidor rodando na porta 3000"));
```

Para melhorar ainda mais as coisas, vamos remover esse código de iniciar o servidor do index.js e vamos colocar ele no novo arquivo, chamado boot.js que fica dentro do diretório config.

```javascript
// Código do arquivo /config/boot.js
module.exports = app => {
    app.listen(3000, () => {;
        console.log("Servidor rodando na porta 3000");
    });
}
```

Agora em index.js, você precisa fazer o consign carregar o boot,js, para isso basta adicionar o seguinte código: 

```javascript
consign()
    .include("routes")
	.then("config/boot.js")
    .into(app);
```

Agora inicie o servidor e veja se tudo está funcionando normalmente. 

#### Trabalhando com Mongo

Chegou a hora de fazer a coisa ficar mais interessante, vamos adicionar um banco de dados na história, o escolhido para esse projeto é o MongoDB, o banco NoSQL mais popular do mercado. 

Trabalhar com Mongo no Node é bastante simples, primeiro vamos começar instalando um módulo especificamente para isso, é o moongose, para isso execute: 

> $  npm install mongoose --save

Com o moongose instalado, se conecte ao mongo e crie um banco de dados, no meu caso chamei ele de livrosapi. Depois de criar o banco vamos criar o arquivo **banco.js** dentro de **config**, aonde vamos criar o código de conexão com o banco. 

```javascript
//Código do arquivo /config/banco.js
var mongoose = require('mongoose');
const url = 'mongodb://localhost/livrosapi';

module.exports = function() {
    mongoose.connect(url, function(err) {
        if(err) throw err;

        console.log("Conectado ao banco com sucesso");
    });
}
```

Agora precisamos atualizar o **index.js** para que ele carregue o **banco.js**: 

```javascript
consign()
    .include("config/banco.js")
    .then('routes')
    .then("config/boot.js")
    .into(app);
```

Agora você pode iniciar o servidor e se tudo der certo, você vai ver a mensagem de conexão com o banco ser exibida. 

Com o banco conectado, vamos criar o modelo de livros, para isso crie o arquivo **Livro.js** dentro de **/models**. O modelo vai ser a representação da collection livro que será criada 

Primeiro vamos importar o mongoose e os Schema do mongosse, para isso faça: 

```javascript
//Código do arquivo /models/Livro.js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
```

Todo Schema no mongoose é mapeado para uma collection no Mongo, assim se queremos criar uma collection de livros, basta crair um schema desse carinha, para isso faça: 

```javascript
let livroSchema = new Schema({
    nome: String, 
    autor: String, 
    editora: {
        nome: String, 
        email: String, 
    } 
});
```

É possível trabalhar muito mais coisas em um Schema, porém como esse é um projeto simples, não há necessidade de adicionar mais detalhes, mas abaixo deixo o link da documentação oficial do Moongoose, sobre Schemas, aconselho que você dê uma olhada depois, não se preocupe, a documentação é muito boa, cheia de exemplos e com zero enrolação. 

[Schemas](https://mongoosejs.com/docs/guide.html)

Para que possamos usar o nosso schema na aplicação, precisamos exportar ele como um modelo do mongoose, para isso adicione o código abaixo, no final do **Livro.js**:

```javascript
module.exports = mongoose.model("Livro", livroSchema);
```

Um model do Mongoose são construtores sofisticados compilados a partir de schemas, esses carinhas são responsáveis por criar e ler documentos do banco de dados. Para utilizar um model, você vai ver que não há muita diferença do que se faz para usar uma classe JavaScript. 

Agora com nosso modelo criado, vamos trocar o retorno estático do endpoint de livros, por uma consulta a nossa collection de livros, para isso abra o arquivo e primeiro adicione um require para o nosso modelo de livros: 

```javascript
var Livro = require('../models/Livro');
```

Então atualize o GET, adicionando o seguinte código, no lugar do retorno existente: 

```javascript
module.exports = app => {
    app.get("/livros", (req, res) => {
        Livro.find(function(err, livros) {
            if(err) console.error(err);
            res.json(livros);
        });
    });
};
```

Agora pare o servidor e inicie novamente, então acesse **http://localhost:3000/livros**, se tudo deu certo, você vai visualizar como retorno **[]**, isso ocorre pois não há nenhum livro adicionado na collection de livros, porém se você acessar seu banco vai ver que a collection agora foi criada. 

Vamos deixar as coisas mais divertidas, e vamos criar um método POST, para adiçao de novos livros a lista, para isso, no endpoint de livros, adicione o seguinte código: 

```javascript
    app.post("/livros", (req, res) => {
        let livro = new Livro ({
            nome: req.body.nome, 
            autor: req.body.autor, 
            editora : {
                nome: req.body.editora.nome, 
                email: req.body.editora.email 
            }
        });
        livro.save(function(err, resultado){
            if(err) res.send(err); 

            res.sendStatus("200");
        });
    });
```

Como você pode ver, as coisas mudam um pouco em relação ao GET, mas nada de outro mundo. Primeiro criamos um novo livro, e passamos para ele os valores que foram encaminhados na requisição, por meio do "req.body.campo". 

Depois basta fazer um save no nosso livro, que o mongosse vai se encarregar de salvar ele no banco, o save porém precisa receber uma function de callback, que no nosso caso vai enviar em caso de erro, o log do erro, ou em caso de sucesso o status ok, para quem fez a requisição.

Porém para que esse código funcione, é necessário instalar o módulo **body-parser**, que é responsável por fazer parser de objetos JSON, para isso execute: 

> $ npm install body-parser --save

E então altere o index.js, fazendo com que o body-parser seja usado: 

```javascript
var express = require('express');
var consign = require('consign');
var bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.json());

consign()
    .include("config/banco.js")
    .then('routes')
    .then("config/boot.js")
    .into(app);
```

Para testar se tudo está funcionando você vai precisar reinciar o servidor e então fazer uma requisição do tipo POST. Para realizar requisições de teste como esse, gosto de utilizar o plugin [Rest Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client), porém você pode utilizar o Postman ou qualquer outra apkicação que lhe agrade mais. 

Uma requisição de teste  para nossa aplicação seria algo como: 

```json
POST http://localhost:3000/livros HTTP/1.1
content-type: application/json

{
    "nome": "E não sobrou nenhum",
    "autor": "Agatha Christie", 
    "editora" : {
        "nome" : "Globo Livros", 
        "email" : "globoLivros@globo.com"
    }
}
```

Se tudo funcionou como deveria, você vai receber uma resposta como essa: 

```http
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/plain; charset=utf-8
Content-Length: 2
ETag: W/"2-nOO9QiTIwXgNtWtBJezz8kv3SLc"
Date: Sun, 02 Sep 2018 03:56:57 GMT
Connection: keep-alive

OK
```

Se você verificar no mongo, vai ver que um livro foi adicionado. 

```json
{
    "_id" : ObjectId("5b8b5f88ff64f356216f36d0"),
    "editora" : {
        "nome" : "Globo Livros",
        "email" : "globoLivros@globo.com"
    },
    "nome" : "E não sobrou nenhum",
    "autor" : "Agatha Christie",
    "__v" : 0
}
```

Repita o processo de adição para gerar massa de dados, adicione pelo menos três livros. 

Agora vamos crair um GET para retornar apenas um livro, com base no id passado na URL, para isso faça: 

```javascript
    app.get("/livros/:id", (req, res) => {
        Livro.find({_id: req.params.id}, function(err, resultado){
            if(err) res.send(err);

            res.json(resultado);
        });
    });
```

A única diferença aqui em relação ao outro GET que criamos antes, é que estamos passando um parâmetro pro find, o _id, fazendo com que a consulta seja filtrada por esse parâmetro. Quando nada é passado todos os elementos da collection serão retornados. 

Bastante parecido com o POST por sua vez, o PUT é utilizado para atualizar um ou mais registros, para implementar esse cara, basta adicionar o código abaixo: 

```javascript
    app.put("/livros/:id", (req, res)=> {
        Livro.findByIdAndUpdate(req.params.id, { 
                nome: req.body.nome, 
                autor: req.body.autor, 
                editora: {
                    nome: req.body.editora.nome,
                    email: req.body.editora.email
                }
            }, function(err){
            if(err) res.send(err);
            res.sendStatus("200");
        }); 
    });
```

Repare no **findByIdAndUpdate** utilizado, essa é uma função muito bacana do mongoose, ele vai fazer a consulta do objeto pelo id passado como parâmetro e já vai fazer o update conforme os campos passados no body. 

Para fechar um CRUD completo falta o DELETE e esse é bem simples de se fazer, para isso faça: 

```javascript
    app.delete("/livros/:id", (req, res)=>{
        Usuario.deleteOne({_id: req.params.id}, function(err){
            if(err) res.sendStatus("401");

            res.sendStatus("200");
        });
    });
```

A única coisa de diferente aqui foi a utilização de deleteOne(), usado justamente para deletar um registro que corresponda ao valor passado como parâmetro. Como passamos o _id, que é um campo único, poderiamos utilizar o delete() ao invés do deleteOne(), pois em teoria nunca devem existir dois objetos com o mesmo id, porém o deleteOne() é mais seguro garantino que nunca mais de um registro seja removido. 

Ao final de tudo, o código completo fica assim: 

```javascript
var Livro = require('../models/Livro');

module.exports = app => {
    app.get("/livros", (req, res) => {
        Livro.find(function (err, livros) {
            if (err) console.error(err);
            res.json(livros);
        });
    });

    app.post("/livros", (req, res) => {
        let livro = new Livro({
            nome: req.body.nome, 
            autor: req.body.autor, 
            editora: {
                nome: req.body.editora.nome,
                email: req.body.editora.email
            }
        });
        livro.save(function (err, resultado) {
            if (err) res.send(err);

            res.sendStatus("200");
        });
    });

    app.get("/livros/:id", (req, res) => {
        Livro.find({_id: req.params.id}, function(err, resultado){
            if(err) res.send(err);

            res.json(resultado);
        });
    });

    app.put("/livros/:id", (req, res)=> {
        Livro.findByIdAndUpdate(req.params.id, { 
                nome: req.body.nome, 
                autor: req.body.autor, 
                editora: {
                    nome: req.body.editora.nome,
                    email: req.body.editora.email
                }
            }, function(err){
            if(err) res.send(err);
            res.sendStatus("200");
        }); 
    });

    app.delete("/livros/:id", (req, res)=>{
        Usuario.deleteOne({_id: req.params.id}, function(err){
            if(err) res.sendStatus("401");

            res.sendStatus("200");
        });
    });
};
```

Você também pode encontrar o projeto completo no meu GitHub, clicando [aqui.](https://github.com/Hallessandro/api-livros)

Bem isso é tudo por hora pessoal, espero que esse post tenha sido útil e qualquer coisa estou a disposição nas redes sociais. Vlw, flw! 