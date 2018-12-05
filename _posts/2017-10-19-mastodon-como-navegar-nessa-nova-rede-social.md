---
title: Mastodon&colon; como navegar nessa nova rede social
date: 2017-10-19T20:31:48+00:00
author: Lond
layout: post
lang: pt
permalink: /2017/10/19/mastodon-como-navegar-nessa-nova-rede-social/
tags:
  - Mastodon
  - Redes sociais
  - Descentralização
  - Código aberto
  - Decentralization
  - Open Source
  - Twitter
  - Social Network
---
<figure><img alt="" src="/assets/2017-10-19-mastodon-main.png" /><figcaption>Sobre toots, servidores e emojis customizados</figcaption></figure>

_(atualizado pela última vez em 4 de dezembro de 2018)_

Talvez você tenha ouvido falar do Mastodon, há alguns meses atrás a rede social bombou na mídia internacional como a rede que veio pra sacudir o Twitter. Mas talvez não, porque a cobertura na mídia nacional foi bem pequena. Ainda assim, a rede está chegando na versão 2.7 e está chegando aos 1.7 milhão de usuários, além de mais de 2400 servidores ativos.

O Mastodon é uma rede social de *microblogging*, semelhante ao Twitter. A sua proposta é ser local onde os seus usuários podem postar status de até 500 caracteres. Até aí, tudo bem igual ao Twitter.

A diferença começa no modelo da rede, que é mais semelhante ao serviço de email, com vários servidores que se comunicam, do que ao modelo do twitter de um grande servidor com todo mundo dentro.

---

### Começando pela parte difícil: como funcionam os servidores?

<figure><img alt="" src="/assets/2017-10-19-mastodon-elephants.png" /><figcaption>Vamos pegar a imagem bonitinha do joinmastodon.org</figcaption></figure>

O Mastodon é composto por vários servidores. Tem o {% external_link {"text":"mastodon.social", "link":"https://mastodon.social"} %}, que é mantido pelo líder do projeto, o {% external_link {"text":"Eugen Rochko", "link":"https://mastodon.social/@gargron"} %}. Ou mesmo o {% external_link {"text":"Mastodon(te)", "link":"https://masto.donte.com.br"} %}, mantido por mim mesmo. Os dois estão em lugares diferentes, controlados por pessoas diferentes, mas ainda assim, eles falam entre si. Se eu quero mandar uma mensagem pro Eugen, basta eu mandar uma mensagem pra `@gargron@mastodon.social` e ele vai receber ela por lá e se ele quiser me responder ele vai responder pra `@renatolond@masto.donte.com.br` e eu vou receber ela de cá. Ou seja, em vez de ser só uma arroba, você é uma arroba em um endereço, que nem email.

Assim como no Twitter no início dos tempos, é possível acompanhar uma timeline especial, a timeline local, que tem todos os toots…

---

Peraí. Eu num disse isso, né? Quando alguém posta uma coisa no Mastodon isso se chama um toot, se pronuncia “Tut”.

<figure><img alt="" src="/assets/2017-10-19-mastodon-toot.jpeg" /><figcaption>Toot é a onomatopeia de uma corneta em inglês. fonte: <a href="https://www.toastmonster.com/2015/01/new-year-toot-toot/">toastmonster</a></figcaption></figure>

---

Então, como eu ia dizendo, é possível acompanhar uma timeline especial onde tem todos os toots públicos dos usuários do seu servidor. É uma maneira bem legal de descobrir gente e conteúdo novo.

E aí, tem a timeline global (também chamada de federada) que é onde estão os toots de todos os usuários que são vistos pela servidor onde você está. Pode ser meio confuso, porque tem gente do mundo todo postando. Tem umas ferramentas pra filtrar línguas nas timelines local e global pra ajudar um pouco nesse sentido.

#### Pô, mas aí só me complicou. Qual a vantagem?

A vantagem é que cada servidor é administrado por gente diferente. Você com certeza pode achar um servidor onde você vai estar livre de conteúdo que você não quer ver e ver mais do que você quer. Tá querendo um servidor feito para brasileiros? {% external_link {"text":"Tem lá", "link":"https://masto.donte.com.br"} %}. Quer um servidor mais voltado pro público LGBTQ? {% external_link {"text":"Tem lá", "link":"https://lgbt.io"} %}. Ou de repente cê tá procurando um servidor mais voltado pro público interessado em livros e {% external_link {"text":"também tem lá", "link":"https://booktoot.club"} %}. E se quiser derrubar o capitalismo e falar de gatinhos, {% external_link {"text":"também tem um cantinho", "link":"https://anticapitalist.party"} %}.

O que você vê na timeline local vai variar bastante de servidor pra servidor. O que você vê na global vai variar porque servidores podem bloquear conteúdo de outros servidores. Então se você está num servidor que não permite nazismo, fascismo e afins, você provavelmente não vai ver conteúdo desse tipo na sua timeline (e se aparecer, você pode reportar aos administradores e eles provavelmente vão bloquear).

E no final das contas, todo mundo com conhecimento técnico ou um pouco de dinheiro pode botar um servidor novo no ar. Então se você quer fazer um servidor pra fãs do campeonato brasileiro, você também pode. (Tô jogando no ar. Acho que ainda não tem, hein. Corre lá :)

#### Ah, mas é tipo reddit então?

Não muito, o reddit tem vários fóruns, mas todos são desconectados. No Mastodon você pode seguir gente de todos os servidores, a diferença é só que gente que está no mesmo servidor que você é mais fácil de acompanhar.
Alguns servidores até são temáticos (pra agregar gente falando de desenvolvimento de jogos ou de tecnologia), mas não é necessariamente o caso em todos os servidores. Na maioria das vezes o tema do servidor vai ajudar só a juntar gente que pensa do mesmo jeito, mas muitas vezes o servidor existe porque tem um nome de domínio maneiro.

#### Tá, e como eu escolho meu servidor, então?

Tem um site que tem um pequeno questionário pra te ajudar justamente nessa questão, o {% external_link {"text":"Mastodon Instances", "link":"https://instances.social/"} %}.

Uma coisa importante do servidor é que a administração e moderação é por servidor. Então o quão rígida ou não vai ser a moderação vai depender do servidor que você escolher. É importante dar uma lida nas regras do servidor pra não ser pego de surpresa ao violar uma delas!

Outra coisa importante é que por não ter uma grande empresa por trás de cada instância, é bom dar uma conferida em quanto tempo o servidor está no ar e se ele não costuma sair do ar com frequência, dá pra ter uma idéia usando o {% external_link {"text": "fediverse network", "link": "https://fediverse.network/masto.donte.com.br/"} %}, que mostra um gráfico de disponibilidade dos últimos 30 dias. O site também mostra quando a instância foi descoberta, mas o serviço começou a funcionar no fim de abril/2018, então tem instância que tá listada por volta dessa data mas já existia antes.

Não se preocupe de escolher o melhor servidor logo de cara. Você pode exportar seus dados e ir pra um outro servidor se você não curtir alguma coisa do servidor em que você está.

---

#### Toots e tweets

No Twitter ou o seu perfil é fechado e aí ninguém vê seus tweets, ou ele é aberto e todo mundo vê seus tweets. No mastodon tem um controle mais fino disso. Você pode ter uma conta fechada e ainda postar toots pra todo mundo ver, quando quiser.

Além disso, no Mastodon tudo vem sempre em ordem cronológica, e nenhum like dos amiguinhos aparece no meio da sua timeline. Você escolhe o que você quer ver, e ninguém vê os posts que você curte, seus favoritos são sempre privados.

Olha as diferenças entre os toots, no mastodon, e os tweets:

* Os toots podem ter até 500 caracteres[⁽¹⁾](#500-chars);
* Os toots têm configurações de privacidade:
  * Você pode postar publicamente (ou seja, todo mundo vê seu toot e ele aparece nas timelines local e global)
  * Você pode postar não listado (ou seja, todo mundo pode ver seu toot, mas ele não aparece nas timelines local e global)
  * Você pode postar privado (e nesse caso seu toot só aparece pra quem te segue)
  * Você pode postar um toot diretamente pra alguns usuários, e nesse caso é parecido com uma mensagem, só os usuários que você citar vão ver.
* Spoiler / alerta de conteúdo: Isso é mara. Você pode marcar enquanto for postar um aviso de conteúdo pra um toot. Aí aparece assim:
  <figure><img alt="" src="/assets/2017-10-19-mastodon-spoiler.png" /><figcaption>Cuidado. Contém spoilers!</figcaption></figure>


---

### Emojis

Desde a versão 2.0 tem uma parada que eu acho particularmente bem legal: emojis customizados!

<iframe src="https://masto.donte.com.br/@renatolond/100627452094203608/embed?autoplay=1" class="mastodon-embed" style="max-width: 100%; border: 0" width="400"></iframe><script src="https://masto.donte.com.br/embed.js" async="async"></script>

Além dos emojis normais que você acha no seu telefone, os administradores das instâncias podem adicionar outros emojis.

---

### Apagar & usar como rascunho

Imagina que você acabou de fazer aquele toot maneiro e assim que ele foi postado, você notou um erro. Não dá pra editar toots, mas dá pra clicar em "apagar & usar como rascunho". Isso apaga o toot e manda ele de volta pra caixa de edição junto com as mídas que estavam nele pra você poder corrigir e postar outra vez.

<figure><img alt="Uma imagem de um toot, com uma foto de um mastodonte segurando a bandeira brasileira e o texto diz 'Olha que bonito esse elefante!'" src="/assets/2017-10-19-mastodon-erro.png" /><figcaption>Epa. Isso não é um elefante.</figcaption></figure>
<figure><img alt="A mesma imagem, mas com um menu de opções abertos onde a opção 'Apagar & usar como rascunho' está selecionada'" src="/assets/2017-10-19-mastodon-erro-2.png" /><figcaption>Vou corrigir!</figcaption></figure>
<figure><img alt="A caixa de edição do Mastodon com o texto 'Olha que bonito esse elefante!' e a imagem do mastodonte segurando a bandeira brasileira" src="/assets/2017-10-19-mastodon-erro-3.png" /><figcaption>Ah, agora dá pra corrigir e botar mastodonte :)</figcaption></figure>

Eu uso isso um monte pra adicionar descrição de texto nas imagens, por exemplo. É super prático!

Isso existe em alguns clientes do Twitter também, mas no Mastodon tem direto pela interface padrão.

---

### Aplicativos

Sim, tem aplicativos pra Android, pra IOS, pra desktop e até mesmo pra uns certos editores de texto 😉

Por exemplo, pra Android os mais comuns são o {% external_link {"text":"Tusky", "link":"https://tuskyapp.github.io/"} %}, {% external_link {"text":"Twidere", "link":"https://github.com/TwidereProject/Twidere-Android"} %} (que funciona tanto pro Mastodon quanto pro Twitter), {% external_link {"text":"Mastalab", "link":"https://github.com/stom79/mastalab"} %}, {% external_link {"text":"Subway Tooter", "link":"https://play.google.com/store/apps/details?id=jp.juggler.subwaytooter"} %} e {% external_link {"text":"11t", "link":"https://github.com/jeroensmeets/mastodon-app"} %}.

Pra iOS o {% external_link { "text": "Toot!", "link": "https://itunes.apple.com/app/toot/id1229021451?ls=1&mt=8" } %}, {% external_link {"text":"Amaroq", "link":"https://itunes.apple.com/us/app/amaroq-for-mastodon/id1214116200"} %} e {% external_link {"text":"iMast", "link":"https://itunes.apple.com/jp/app/imast/id1229461703"} %}.

Além disso, ambos Android e iOS recentemente suportam {% external_link {"text":"PWAs", "link":"https://pt.wikipedia.org/wiki/Progressive_Web_App"} %} e por isso você pode usar o próprio site da sua instância como um app no seu celular.

Pra outros sistemas e uma lista mais atualizada, dá pra dar uma olhada nessa lista aqui que é mantida pelo projeto: {% external_link {"text":"aplicativos", "link":"https://github.com/masto-donte-com-br/documentation/blob/master/Using-Mastodon/Apps.md"} %}.

Como o Mastodon é open-source, a maioria dos seus aplicativos também é. Então você pode dar uma procurada até encontrar um app que te faça se sentir mais em casa.

<h3>Ferramentas</h3>

Mudar de rede social é um negócio complicado e é por isso que tem ferramentas pra tentar ajudar um pouco na transição.

{% external_link {"text":"Mastodon Bridge (a ponte)", "link":"http://bridge.mastodon.social"} %}: Criado pelo próprio {% external_link {"text":"Eugen Rochko", "link":"https://mastodon.social/@gargron"} %}, a ponte serve pra descobrir amigos do Twitter no Mastodon e vice-versa. Depois de criar sua conta em um dos servidores, basta ir lá e conectar a sua conta do Twitter e do Mastodon. Aí ele vai mostrar onde você pode seguir seus amigos do Twitter.

{% external_link {"text":"Mastodon Twitter Crossposter (postando entre as redes)", "link":"http://crossposter.masto.donte.com.br"} %}: Essa aí é minha. Você conecta suas contas do Twitter e do Mastodon e aí você pode decidir como você quer postar entre as redes. Do Twitter pro Mastodon, ou do Mastodon pro Twitter, que tipo de posts vão ser postados. É open-source e tem coisa pra fazer, se quiser contribuir.


### Segurança de dados

Quando você se inscreve em um servidor do Mastodon (vamos dizer, no {% external_link {"text":"masto.donte.com.br", "link":"https://masto.donte.com.br"} %}), seus dados ficam registrados no masto.donte.com.br. O administrador do servidor pode ver suas mensagens, assim como o Gmail também pode ver suas mensagens. O Mastodon por padrão não permite que administradores vejam messagens marcadas como privadas, mas através de denúncias ou olhando o conteúdo do banco de dados, mesmo as mensagens privadas podem ser visualizadas.

Quando alguém de outro servidor (digamos, do {% external_link {"text":"mastodon.social", "link":"https://mastodon.social"} %}) te segue ou se você enviar uma mensagem pra um usuário que esteja por lá, os seus posts são enviados também para esse outro servidor e uma cópia desses posts vai ser guardada lá.

Isso quer dizer que administradores de servidores em que você tenha seguidores ou pra quem você envia mensagens podem espiar as mensagens. É exatamente o mesmo caso de servidores de email, se você enviar uma mensagem pra alguém no servidor do trabalho dessa pessoa, a empresa poderia ver as mensagens.

Na prática é tão (in)seguro quanto outras redes sociais.

### Mais informações

A página do projeto é um bom ponto pra começar: {% external_link {"text":"The Mastodon Project", "link":"http://joinmastodon.org"} %}. Tem tradução em português por lá. Aliás, falando em tradução: tanto a página do projeto quanto a interface do Mastodon em si foram traduzidas pro português Brasileiro pela {% external_link {"text":"Anna", "link":"https://anna.flourishing.stream"} %} 🎉

Tem muito mais informação, muito mais detalhada, no {% external_link {"text":"repositório de dosumentação do projeto", "link":"https://github.com/tootsuite/documentation"} %}, mas a maioria das coisas ainda não está traduzida pra português ou português do Brasil. (Tá aí uma oportunidade, ó.)

Um pouco mais velho mas igualmente útil é o texto da Qina Liu: {% external_link {"text":"What I wish I knew before joining Mastodon", "link":"https://hackernoon.com/what-i-wish-i-knew-before-joining-mastodon-7a17e7f12a2b"} %}. Embora esteja desatualizado em alguns pontos, ainda é bem divertido e foi o que me inspirou a escrever esse aqui :)

Um outro também que explica bem vários pontos que eu tento explicar por aqui é o texto da Ginny McQueen: {% external_link {"text":"Toot How-To : Intro to Mastodon", "link":"https://medium.com/@GinnyMcQueen/toot-how-to-intro-to-mastodon-e5655bfa87d2"} %}.

Sabe tudo que eu falei sobre instâncias diferentes do Mastodon? O Mastodon na verdade está no Fediverso, e ele não é o único software por lá. Dá uma olhada em mais informações sobre o Fediverso {% external_link { "text": "por aqui", "link": "https://en.wikipedia.org/wiki/Fediverse" } %}.

---

<a name='500-chars'></a>[1]: Vale notar que por padrão os toots têm 500 caracteres. Na prática alguns servidores permitem mais, no finado {% external_link {"text":"witches.town", "link":"https://web.archive.org/web/20180417044653/https://witches.town/about"} %}, por exemplo, o limite era de 666 caracteres. 😜
