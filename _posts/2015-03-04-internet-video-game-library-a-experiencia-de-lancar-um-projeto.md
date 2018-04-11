---
id: 938
title: 'Internet Video Game Library: a experiência de lançar um projeto'
date: 2015-03-04T20:37:59+00:00
author: Lond
layout: post
guid: /?p=938
permalink: /2015/03/04/internet-video-game-library-a-experiencia-de-lancar-um-projeto/
categories:
  - Random Thoughts
tags:
  - Developments
  - Nerdish
  - Random Thoughts
---
Um dos meus projetos mais velhos finalmente está no ar e eu acho que vale a pena falar um pouco sobre a experiência.

# Uma introdução

No ensino médio conheci um amigo que guardava planilhas com os jogos que ele tinha, os que ele já tinha terminado e os que tinha emprestado.
  
Nessa época comecei a guardar os meus em uma também, mas em 2003 planilhas eram coisas muito etéreas, quando formatar seu SO (win.. cof.. dows.. cof.. cof..) eram coisas rotineiras, era fácil perder uma por descuido. E várias vezes perdi o conteúdo delas.
  
Comecei a ler mais portais de jogos e acabei desenvolvendo alguns métodos, ainda que primitivos, de guardar que jogos eu tinha jogado, quais eu queria em alguns desses, principalmente o gamespot.

A internet evoluiu desde então, e com isso, alguns novos serviços apareceram. Conheci sites e tracking de outras coisas: livros, filmes, seriados, cerveja, vinho, lugares. Usei todos os sistemas de tracking de jogos que eu conheci pelo caminho: Raptr, PlayFire, Backloggery, HowLongToBeat, Alvanista, EstouJogando. Nenhum deles me deixou muito feliz, até que recentemente eu voltei a usar planilhas (dessa vez, do Google Drive) pra manter meus jogos e quando eu os terminei.

# Conhecendo o Goodreads

Em 2012 conheci o Goodreads. Na época, usava o skoob pra guardar os livros que eu lia. Achei o sistema incrível, diversas edições, suporte a várias línguas, ratings unificados. Era tudo que eu queria pra um site de jogos.

# A difícil criação do Internet Video Game Library

O IVGLib ficou em gestação algumas vezes. A primeira vez tentei usar o Google App Engine para fazer, mas java nunca foi minha praia e eu entrei no barco durante os meses que seguiram uma atualização _major_ na plataforma. Na época, o projeto tinha o codinome SEMAG. E com isso ele ficou de lado.

Um tempo depois, resolvi tentar retomar o projeto, dessa vez usando algum framework de PHP. Li sobre alguns, tentei usar o FuelPHP, e mais uma vez a falta de documentação, algumas frustrações pra fazer coisas que eu achava que eram básicas acabaram me fazendo mais uma vez largar o projeto de lado.

Do meio do ano passado pra cá eu vinha tentando aprender Ruby on Rails, fazendo homeopaticamente o tutorial do ruby.railstutorial.org e a parada foi fluindo. Em janeiro, durante as minhas férias, finalmente recomecei o projeto, dessa vez em Rails.

# Desenvolvimento e tecnologias

Rails é um negócio incrível, você pensa em fazer uma parada e tem uma Gem pra fazer isso. (o que também é verdade pra muitas linguagens mais novas, antes que me joguem pedras).

Assim que comecei a fazer o sistema e me animei, registrei o domínio (um monte deles, na verdade), defini um _MVP_ e saí fazendo a parada. Passei parte das minhas férias de janeiro debruçado sobre o PC fazendo o início do sistema.

Atualmente, o sistema tá uma sopa de nomes de serviços e aplicações: Tô hospedando o código no _Heroku_, com a busca usando o _ElasticSearch_ através do _SearchBox_, usando coisas do _Amazon AWS_ pra armazenamento de imagens e etc.

É muito doido ficar nessa de _DevOps_, nunca tinha ficado nessa posição antes e tá sendo uma experiência bem curiosa.

<figure>
<img src="http://i.imgur.com/JPnYWL3.gif" alt="Go Live Day, by DevOps Reactions" width="275" height="189" />
<figcaption>Go Live Day, by DevOps Reactions</figcaption>
</figure>

Apesar disso, meu MVP tá lá. Mil e umas funcionalidades legais pra implementar nos próximos dias. Diversos jogos pra cadastrar. Enfim, muito trabalho.

Nos próximos dias vai ser tempo de esmagar bugs antes de voltar pro roadmap e implementar os próximos passos. Parece que vai ser um longo e interessante caminho :)
