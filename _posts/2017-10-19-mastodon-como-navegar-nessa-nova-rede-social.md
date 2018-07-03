---
title: Mastodon&colon; como navegar nessa nova rede social
date: 2017-10-19T20:31:48+00:00
author: Lond
layout: post
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

Talvez você tenha ouvido falar do Mastodon, há alguns meses atrás a rede social bombou na mídia internacional como a rede que veio pra sacudir o Twitter. Mas talvez não, porque aparentemente a cobertura na mídia nacional foi bem pequena. Ainda assim, a rede acaba de chegar na versão 2.0 e está alcançando 1 milhão de usuários, além de mais de 1000 servidores ativos.

O Mastodon é uma rede social de *microblogging*, semelhante ao Twitter. A sua proposta é ser local onde os seus usuários podem postar status de até 500 caracteres. Até aí, tudo bem igual ao Twitter.

A diferença começa no modelo da rede, que é mais semelhante ao serviço de email, com vários servidores que se comunicam, do que ao modelo do twitter de um grande servidor com todo mundo dentro.

---

### Começando pela parte difícil: como funcionam os servidores?

<figure><img alt="" src="/assets/2017-10-19-mastodon-elephants.png" /><figcaption>Vamos pegar a imagem bonitinha do joinmastodon.org</figcaption></figure>

O Mastodon é composto por vários servidores. Tem o [mastodon.social](https://mastodon.social){:target="_blank"}, que é mantido pelo líder do projeto, o [Eugen Rochko](https://mastodon.social/@gargron){:target="_blank"}. Ou mesmo o [Mastodon(te)](https://masto.donte.com.br){:target="_blank"}, mantido por mim mesmo. Os dois estão em lugares diferentes, controlados por pessoas diferentes, mas ainda assim, eles falam entre si. Se eu quero mandar uma mensagem pro Eugen, basta eu mandar uma mensagem pra `@gargron@mastodon.social` e ele vai receber ela por lá e se ele quiser me responder ele vai responder pra `@renatolond@masto.donte.com.br` e eu vou receber ela de cá. Ou seja, em vez de ser só uma arroba, você é uma arroba em um endereço, que nem email.

Assim como no Twitter no início dos tempos, é possível acompanhar uma timeline especial, a timeline local, que tem todos os toots…

---

Peraí. Eu num disse isso, né? Quando alguém posta uma coisa no Mastodon isso se chama um toot, se pronuncia “Tut”.

<figure><img alt="" src="/assets/2017-10-19-mastodon-toot.jpeg" /><figcaption>Toot é a onomatopeia de uma corneta em inglês. fonte: <a href="https://www.toastmonster.com/2015/01/new-year-toot-toot/">toastmonster</a></figcaption></figure>

---

Então, como eu ia dizendo, é possível acompanhar uma timeline especial onde tem todos os toots públicos dos usuários do seu servidor. É uma maneira bem legal de descobrir gente e conteúdo novo.

E aí, tem a timeline global (também chamada de federada) que é onde estão os toots de todos os usuários que são vistos pela servidor onde você está. Pode ser meio confuso, porque tem gente do mundo todo postando. Tem umas ferramentas pra filtrar línguas nas timelines local e global pra ajudar um pouco nesse sentido.

#### Pô, mas aí só me complicou. Qual a vantagem?

A vantagem é que cada servidor é administrado por gente diferente. Você com certeza pode achar um servidor onde você vai estar livre de conteúdo que você não quer ver e ver mais do que você quer. Tá querendo um servidor feito para brasileiros? [Tem lá](https://masto.donte.com.br){:target="_blank"}. Quer um servidor mais voltado pro público LGBTQ? [Tem lá](https://lgbt.io){:target="_blank"}. Ou de repente cê tá procurando um servidor mais voltado pro público interessado em livros e [também tem lá](https://bookwitty.social){:target="_blank"}. E se quiser derrubar o capitalismo e falar de gatinhos, [também tem um cantinho](https://anticapitalist.party){:target="_blank"}.

O que você vê na timeline local vai variar bastante de servidor pra servidor. O que você vê na global vai variar porque servidores podem bloquear conteúdo de outros servidores. Então se você está num servidor que não permite nazismo, fascismo e afins, você provavelmente não vai ver conteúdo desse tipo na sua timeline (e se aparecer, você pode reportar aos administradores e eles provavelmente vão bloquear).

E no final das contas, todo mundo com conhecimento técnico ou um pouco de dinheiro pode botar um servidor novo no ar. Então se você quer fazer um servidor pra fãs do campeonato brasileiro, você também pode. (Tô jogando no ar. Acho que ainda não tem, hein. Corre lá :)

#### Tá, e como eu escolho meu servidor, então?

Tem um site que tem um pequeno questionário pra te ajudar justamente nessa questão, o [Mastodon Instances](https://instances.social/){:target="_blank"}.

---

### Toots e tweets

Os toots são parecidos com tweets, mas tem algumas diferenças.

* Os toots podem ter até 500 caracteres[⁽¹⁾](#500-chars);
* Os toots têm configurações de privacidade:
  * Você pode postar publicamente (ou seja, todo mundo vê seu toot e ele aparece nas timelines local e global)
  * Você pode postar não listado (ou seja, todo mundo pode ver seu toot, mas ele não aparece nas timelines local e global)
  * Você pode postar privado (e nesse caso seu toot só aparece pra quem te segue)
  * Você pode postar um toot diretamente pra alguns usuários, e nesse caso é parecido com uma mensagem, só os usuários que você citar vão ver.
* Spoiler / alerta de conteúdo: Isso é mara. Você pode marcar enquanto for postar um aviso de conteúdo pra um toot. Aí aparece assim:
  <figure><img alt="" src="/assets/2017-10-19-mastodon-spoiler.png" /><figcaption>Cuidado. Contém spoilers!</figcaption></figure>

Ah, e é claro: Tudo em ordem cronológica. Nada de toot fora de ordem ou like dos amigos aparecendo na timeline.

---

### Emojis

A versão 2.0 está fresquinha, saída do forno! E com ela vem uma novidade que eu acho particularmente bem legal: emojis customizados!

<figure><img alt="" src="/assets/2017-10-19-mastodon-emoji.png" /><figcaption>Tá tendo <a href="http://cultofthepartyparrot.com/">party parrot</a> e várias bandeiras sim!</figcaption></figure>

Além dos emojis normais que você acha no seu telefone, os administradores das instâncias podem adicionar outros emojis.

---

### Aplicativos

Sim, tem aplicativos pra Android, pra IOS, pra desktop e até mesmo pra uns certos editores de texto 😉

Por exemplo, pra Android os mais comuns são o [Tusky](https://tuskyapp.github.io/){:target="_blank"}, [Twidere](https://github.com/TwidereProject/Twidere-Android){:target="_blank"} (que funciona tanto pro Mastodon quanto pro Twitter), [Mastalab](https://github.com/stom79/mastalab){:target="_blank"}, [Subway Tooter](https://play.google.com/store/apps/details?id=jp.juggler.subwaytooter){:target="_blank"} e [11t](https://github.com/jeroensmeets/mastodon-app){:target="_blank"}.

Pra iOS o [Amaroq](https://itunes.apple.com/us/app/amaroq-for-mastodon/id1214116200){:target="_blank"} e [iMast](https://itunes.apple.com/jp/app/imast/id1229461703){:target="_blank"}.

Além disso, ambos Android e iOS recentemente suportam [PWAs](https://pt.wikipedia.org/wiki/Progressive_Web_App){:target="_blank"} e por isso você pode usar o próprio site da sua instância como um app no seu celular.

Pra outros sistemas e uma lista mais atualizada, dá pra dar uma olhada nessa lista aqui que é mantida pelo projeto: [aplicativos](https://github.com/masto-donte-com-br/documentation/blob/master/Using-Mastodon/Apps.md){:target="_blank"}.

Como o Mastodon é open-source, a maioria dos seus aplicativos também é. Então você pode dar uma procurada até encontrar um app que te faça se sentir mais em casa.

<h3>Ferramentas</h3>

Mudar de rede social é um negócio complicado e é por isso que tem ferramentas pra tentar ajudar um pouco na transição.

[Mastodon Bridge (a ponte)](http://bridge.mastodon.social){:target="_blank"}: Criado pelo próprio [Eugen Rochko](https://mastodon.social/@gargron){:target="_blank"}, a ponte serve pra descobrir amigos do Twitter no Mastodon e vice-versa. Depois de criar sua conta em um dos servidores, basta ir lá e conectar a sua conta do Twitter e do Mastodon. Aí ele vai mostrar onde você pode seguir seus amigos do Twitter.

[Mastodon Twitter Crossposter (postando entre as redes)](http://crossposter.masto.donte.com.br){:target="_blank"}: Essa aí é minha. Você conecta suas contas do Twitter e do Mastodon e aí você pode decidir como você quer postar entre as redes. Do Twitter pro Mastodon, ou do Mastodon pro Twitter, que tipo de posts vão ser postados. É open-source e tem coisa pra fazer, se quiser contribuir.

### Mais informações

A página do projeto é um bom ponto pra começar: [The Mastodon Project](http://joinmastodon.org){:target="_blank"}. Tem tradução em português por lá. Aliás, falando em tradução: tanto a página do projeto quanto a interface do Mastodon em si foram traduzidas pro português Brasileiro pela [Anna](https://anna.flourishing.stream){:target="_blank"} 🎉

Tem muito mais informação, muito mais detalhada, no [repositório de documentação do projeto](https://github.com/tootsuite/documentation){:target="_blank"}, mas a maioria das coisas ainda não está traduzida pra português ou português do Brasil. (Tá aí uma oportunidade, ó.)

Um pouco mais velho mas igualmente útil é o texto da Qina Liu: [What I wish I knew before joining Mastodon](https://hackernoon.com/what-i-wish-i-knew-before-joining-mastodon-7a17e7f12a2b){:target="_blank"}. Embora esteja desatualizado em alguns pontos, ainda é bem divertido e foi o que me inspirou a escrever esse aqui :)

---

<a name='500-chars'></a>[1]: Vale notar que por padrão os toots têm 500 caracteres. Na prática alguns servidores permitem mais, no finado [witches.town](https://witches.town){:target="_blank"}, por exemplo, o limite era de 666 caracteres. 😜
