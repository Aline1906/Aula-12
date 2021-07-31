# Banco de dados MongoDB

## MongoDB é um software de banco de dados orientado a documento livre, de código aberto e multiplataforma. Foi escrito em linguagem C++ e usa documentos semelhantes a JSON.

## Agora que já apresentamos o nosso queridinho do momento, vamos ver o que podemos fazer com ele.

## Apreitamos um JSON de livros feito em aula anterior e demos alguma demanda de negócio para ele:

* Inserir documentos
* Atualizar documentos
* Excluir documentos 
* Consultar
* Consultar utilizando combinação entre os seletores
* Consultar página e ordenada - utilizando skip, limit e sort

## Rotas para a nossa demanda

 ### Buscando Livros

db.getCollection('livros').find({})

### Inserindo um livro

  db.livros.insertMany

### Atualizando a quantidade de páginas do livro

  db.getCollection('livros').update(
    {
       "nome" : "O Mistério da Estrela"
    },
    
    {
        $set:{'pagina': '269'}
    },
    
    {
        "multi" : false
    }
);

### Excluindo um livro

  db.getCollection('livros').remove({
    "categoria": { $ne: "AVENTURA" }
})

### Consulta com projeção -

 Livros de Romance ordenados do maior para o menor número de páginas
  db.getCollection('livros').find({categoria:'Romance'}).sort({pagina: 1})

### Consulta combinando informações -

 Livros de Aventura com mais de 100 páginas
  db.getCollection('livros').find({'categoria':'Aventura', 'pagina':{$gt:100}})

### Consulta ordenada com (skip, limit e sort) -

 Livro de Aventura com a terceira menor quantidade de páginas
db.getCollection('livros').find({'categoria':'Aventura'}).sort({pagina: 1}).skip(2).limit(1)