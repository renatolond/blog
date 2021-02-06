---
layout: post
title: O guia paranóico de segurança em tempos digitais
lang: pt
---

_(atualizado pela última vez em 6 de fevereiro de 2021)_

Com a escalada do fascismo e o fato de que nossas vidas estão cada vez mais presentes online, é preciso tomar precauções para que nossas identidades digitais não caiam nas mãos erradas. Primeiro porque isso pode revelar informações valiosas nossas e de pessoas queridas à nossa volta. Segundo porque isso pode permitir que atacantes passem informações falsas usando nossas identidades.

Esse post está dividido em duas partes: uma parte de dicas mais gerais e uma parte de recomendações de apps pra substituir.

As recomendações estão num formato em que você pode passar rapidamente o olho e ver os apps recomendados, seguido pelo porque dos outros apps não serem recomendados e por fim uma pequena explicação do porque os apps recomendados estarem na lista.

No geral, ao longo desse guia, uma coisa é recorrente: evite os conglomerados tecnológicos. Google e Facebook sobrevivem de coletar seus dados e seus aplicativos coletam a maior quantidade de dados possíveis. Além disso, evite aplicativos e redes que não encriptam seus dados, porque seus dados podem ser divulgados tanto por causa de vulnerabilidades, quanto por outros meios (por exemplo, podem ser acessados por empregados das empresas e vendidos pra quem paga mais).

Segurança digital é uma luta constante e é preciso se acostumar a ter todos os ítens na cabeça. Mesmo que você resolva adotar todas as sugestões que eu comento por aqui, vai levar um tempo até isso estar naturalizado. Não desista porque uma coisa ou outra ainda não está de acordo com esse guia (ou com outros guias de segurança que você pode encontrar por aí).

Esse guia é mais um dentre outros guias que podem ser encontrados na internet. Posts como {% external_link {"text":"Um manual de segurança digital para tempos sombrios", "link":"https://medium.com/revista-subjetiva/um-manual-de-seguran%C3%A7a-digital-para-tempos-sombrios-2d414d0a3f24"} %} e livros como {% external_link {"text":"Queer Privacy: Essays From The Margins Of Society", "link":"https://www.goodreads.com/book/show/35105309-queer-privacy"} %} foram usados como referências para esse post.

Se quiser fazer uma correção nesse post ou discutir algum ponto, só entrar em contato por um dos meios disponíveis ali no link [sobre](/about), ou ainda, abrir uma discussão direto no [github](https://github.com/renatolond/blog/issues)

Tenha em mente: esse post não é revisado com frequência, antes de usar cegamente um dos apps daqui, dê uma pesquisada rápida para ver o status atual do aplicativo. Muita coisa muda o tempo todo :)

---

<nav markdown="1">
  <h3 class="toc_title">Nessa página</h3>
  1. test
  {:toc}
</nav>

---

## Dicas gerais

### Webcam e microfone

Podem parecer dicas batidas, mas cubra a sua webcam quando não estiver usando. A solução barata é um post-it na frente da câmera, mas existem alguns adesivos especialmente para esse fim que facilitam caso você usa a sua câmera com frequência para chamadas, que deslizam pra cubrir a câmera, dá pra achar por uns R$10 pela internet.

No caso do microfone, as instruções variam de modelo pra modelo, mas o conselho é o mesmo, desligue quando não estiver usando. Alguns notebooks tem um botão pra dar mute no microfone, outros não são tão fáceis.

Nos dois casos a idéia é evitar capturas indesejadas.

### Autenticação em dois passos

A autenticação em dois passos (conhecida como 2FA, do inglês _2-factor authentication_) deve ser ligada para todos os serviços possíveis. Evite usar autenticação em dois passos que dependa de recepção de SMS, prefira aplicativos que gerem a autenticação baseada em tempo, como o FreeOTP (alguns gerenciadores de senha tem essa opção, também).

Com a autenticação em dois passos ativada, para alguém ter acesso à uma das suas contas, além de ter acesso a sua senha, o atacante também deve ter acesso ao seu aplicativo gerador, o que dificulta bastante o acesso.

A autenticação por SMS sofre do problema de estar vulnerável a clonagem de chip, o que é extremamente comum. A vice escreveu {% external_link {"text":"um artigo, em inglês, sobre a técnica", "link":"https://motherboard.vice.com/en_us/article/vbqax3/hackers-sim-swapping-steal-phone-numbers-instagram-bitcoin"} %}. De maneira curta: os atacantes fazem engenharia social para conseguir clonar os chips de dentro das operadoras. Com isso, conseguem os códigos de confirmação necessários para fazer login. Essa técnica foi usada para derrubar o grupo de facebook "Mulheres contra Bolsonaro", por exemplo.

### Gerenciador de senhas

**Use**: {% external_link {"text":"bitwarden", "link":"https://bitwarden.com/"} %}, {% external_link {"text":"KeePassXC", "link":"https://keepassxc.org/"} %}  
Evite: Salvar suas senhas no navegador

Toda semana tem um site sendo invadido e uma lista de senhas é disponibilizada na internet, listas essas que normalmente são uma combinação de emails e senhas. Usar a mesma senha em diversos sites faz com que haja o risco de que quando um site é atacado, todos os outros sites em que usamos a mesma senha possam então ser invadidos sem esforço algum.

Existem diversas aplicações que geram senhas para nós. A idéia dessas aplicações é que nós mantemos somente uma senha, mais complexa, e não sabemos as outras senhas que utilizamos em outros sites, usando senhas geradas por esses aplicativos que são complexas e individuais para cada site.

Usar um gerenciador de senhas requer uma mudança de mentalidade, para que nunca usemos "aquela" senha que a gente usa em todos os sites pra novos cadastros e pra que pouco a pouco possamos mudar as nossas senhas existentes.

Recomendo começar a mudança com passos de formiguinha: escolha um site que você usa bastante e use o gerenciador de senhas para esse site, e somente para ele, por alguns meses. A ideia é acostumar com o fato de ter que desbloquear o gerenciador e se acostumar de que você não vai saber a senha do site de cabeça e que não há problema nisso. E aí, num segundo passo, é começar a ir mudando senhas em outros sites, sempre usando senhas geradas.

Eu recomendo o {% external_link {"text":"bitwarden", "link":"https://bitwarden.com/"} %}, disponível para a maioria dos sistemas operacionais e browsers, além de sincronizar automaticamente pela internet. Outra boa opção é o {% external_link {"text":"KeePassXC", "link":"https://keepassxc.org/"} %}, que usa um arquivo local e permite mais controle, necessitando de um pouco mais de trabalho no sentido de ter que sincronizar o arquivo semi-manualmente (usando a nuvem para sincronizar automaticamente, ou pendrive e similares).

Não é diretamente relacionado, mas vale lembrar: evite salvar suas senhas no navegador; em alguns casos como no Chrome/Chromium elas são sincronizadas pela internet e é muito fácil de ter acesso indevido à essas senhas, mesmo usando outros navegadores. Mesmo que você decida usar suas próprias senhas, use algum gerenciador de senha pra digitar as senhas automaticamente pra você ao invés de salvar no navegador.

### Redes sem fio sem senha

Muito comum em aeroportos, hotéis e outros lugares públicos em geral, redes sem fio que não tenham senha devem ser evitadas. Todo o tráfego entre o seu computador (ou telefone) e a internet fica em aberto nessas redes. Qualquer um por perto pode capturar esse tráfego e saber os sites que você está acessando e caso o site não use _https_, pode inclusive capturar senhas e outros dados sensíveis.

Pra quando não dá pra escolher, o jeito é usar uma VPN.

### VPNs

VPNs (em português: redes privadas virtuais) são uma camada extra de segurança em cima da sua rede. É como se você estabelecesse um túnel entre o seu dispositivo e o servidor da VPN, e para chegar à internet o tráfego tem de passar por esse túnel.

A vantagem desse tipo de túnel é que todo o tráfego é criptografado entre o seu dispositivo e o servidor, e o servidor pode estar em outros países (passando por bloqueios locais ou censuras a certos serviços). A desvantagem é que todo o seu tráfego vai passar por um servidor de terceiros.

Por esse motivo, VPNs gratuitas devem ser evitadas. Essas VPNs podem ser montadas com o propósito de coletar dados ou de servir malware.

Para uma lista completa, existe a lista do {% external_link {"text":"That One Privacy Site", "link":"https://thatoneprivacysite.net/vpn-section/"} %}, que tem detalhadas comparações entre VPNs comerciais. Algumas recomendações bem cotadas na comparação: {% external_link {"text":"SecureVPN.to", "link":"https://SecureVPN.to"} %}, {% external_link {"text":"Mullvad", "link":"https://www.mullvad.net/"} %}, {% external_link {"text":"ProtonVPN", "link":"https://protonvpn.com/"} %}, {% external_link {"text":"VikingVPN", "link":"https://vikingvpn.com/"} %}.

As assinaturas são meio caras mesmo, mas normalmente as VPNs permitem um número de conexões simultâneas, então dá pra rachar um pacote com pessoas próximas pra baratear.

### Extensões para navegador

A internet atual é baseada em anúncios e redes de anunciantes adoram coletar todos os dados possíveis para cruzar o que nos mostrar. Para evitar esse tipo de rastreamento, o ideal é instalar algumas extensões que diminuem essa exposição, ao menos no computador:

* {% external_link {"text":"uBlock origin", "link":"https://github.com/ialexsilva/uBlock/blob/master/README.md#instala%C3%A7%C3%A3o"} %}: Bloqueia anúncios e coletores de informações mais comuns
* {% external_link {"text":"Privacy Badger", "link":"https://www.eff.org/privacybadger"} %}: Extensão da Eletronic Frontier Foundation, que também bloqueia anúncios e coletores de informações comuns

As duas extensões tem trabalhos semelhantes, mas com frequência bloqueiam coisas diferentes. Trabalhando em conjunto reduzem bastante o número de anúncios e informações que são coletadas por anunciantes.

### Ligue a criptografia do seu celular e computador

Ligar a criptografia no seu celular vai ajudar no caso de perda ou furto, protegendo seus dados contra acesso indevido. Quase todo mundo bota uma senha pra desbloquear o celular, mas isso só protege contra um acesso direto. Encriptar o seu celular vai proteger contra acesso usando um computador e ferramentas para acessar o conteúdo do seu celular, sem nunca passar pela tela de desbloqueio.

Algumas notas:
1. ligar a criptografia pode fazer o seu celular ficar ligeiramente mais lento.
2. para desligar a criptografia é necessário retornar o celular às configurações de fábrica

É possível ligar a criptografia em quase todo telefone Android e em todos os iPhones. As instruções variam de aparelho para aparelho. No Android normalmente a configuração fica localizada na parte de segurança, enquanto no iPhone você precisar criar um código de acesso.

No computador também é possível ligar a criptografia para seus dados, os passos são bem diferentes dependendo da versão do seu sistema operacional, então é bom dar uma olhada na ajuda do seu sistema.

### Celular e protestos

Se alguem tem acesso físico aos seus dispositivos, fica muito mais difícil de se proteger. Um agente mal intencionado pode forçar você a revelar sua senha e ter acesso ao seu dispotivo. Evitar de levar seu celular pra manifestações pode não ser prático ou desejado (afinal, gravar qualquer coisa que esteja acontecendo pode ser uma parada valiosa depois).

Além da dica da criptografia, evite usar sua digital para destravar seu celular (pelo menos, pela duração do protesto).

## O que usar como...

### Mecanismo de Busca
<figure><img alt="Captura de tela da página inicial do DuckDuckGo" src="/assets/2018-10-29_duckduckgo.png" /><figcaption>DuckDuckGo</figcaption></figure>

**Use**: {% external_link {"text":"DuckDuckGo", "link":"https://duckduckgo.com/privacy"} %}, {% external_link {"text":"Searx", "link":"https://asciimoo.github.io/searx/"} %}  
Evite: Google, Bing

O Google armazena todos seus dados de busca, você pode ver todas as buscas que você realizou no google através de um painel de controle localizado em {% external_link {"text":"My Activity", "link":"https://myactivity.google.com"} %}. O que isso quer dizer é que mais uma vez, seus dados podem ser acessados em caso de vulnerabilidade ou funcionários mal intencionados.

O Bing não está muito atrás, e embora tenha menos dados em sua posse, faz parte da Microsoft que não está muito melhor no quesito "gigante da tecnologia que guarda mais dados do que poderia".

{% external_link {"text":"DuckDuckGo", "link":"https://duckduckgo.com/privacy"} %} e {% external_link {"text":"Searx", "link":"https://asciimoo.github.io/searx/"} %} são dois serviços de buscas que tem a privacidade em mente, sem perder a qualidade das buscas.

### Aplicativos de mensagem instantânea

<figure><img alt="Captura de tela de um chat no Signal" src="/assets/2018-10-29_signal.png" height="600" /><figcaption>Signal</figcaption></figure>

**Use**: {% external_link {"text":"Threema", "link":"https://threema.ch/"} %}, {% external_link {"text":"Signal", "link":"https://signal.org"} %}  
Evite: Whatsapp, Facebook Messenger, Google Hangouts, Google Chats, Telegram, Viber, WeChat, DMs no Twitter

Queremos evitar duas coisas no caso de mensagens instantâneas: armazenamento das mensagens nos servidores do aplicativo, porque podem ser recuperadas através de falhas de segurança ou de funcionários mal intencionados; criptografia ponto-a-ponto, para evitar que alguém possa ler as mensagens sem permissão.

O Whatsapp dispõe de criptografia ponto-a-ponto, mas é de propriedade do Facebook e não dá pra ter certeza de quantos metadados o Facebook armazena de todas as conversas.

O Messenger dispõe de "chats secretos", mas o resto das conversas não é encriptada e é armazenada nos servidores do Facebook.

Hangouts e chats não dispõe de comunicação segura e toda a comunicação é armazenada nos servidores do Google.

Viber promete criptografia ponto-a-ponto, mas assim como o Whatsapp, não temos como saber o quão segura é a sua implementação.

Outros aplicativos, tais como WeChat não encriptam suas conversas e devem ser evitados.

O Telegram era minha primeira sugestão durante muito tempo. A interface é a melhor dentre os aplicativos de comunicação, mas o seu design faz com que por padrão as conversas não usem criptografia. Só as conversas criadas como "chat secreto" usam criptografia ponto-a-ponto, o que por consequência faz com que as mensagens de conversas normais sejam todas armazenadas nos servidores do Telegram.

{% external_link {"text":"Threema", "link":"https://threema.ch/"} %} e {% external_link {"text":"Signal", "link":"https://signal.org"} %} encriptam suas mensagens e tem código aberto disponível para inspeção.

Numa versão anterior desse post eu recomendava o Wire, que também é encriptado ponta-a-ponta. Porém, em 2019 o Wire mudou de mãos e agora pertence a uma companhia estadunidense. Essa mudança foi {% external_link {"text": "bastante criticada", "link": "https://www.thinkprivacy.ch/cutting-the-wire/"} %} pela falta de transparência e por vir junto com {% external_link {"text": "mudanças suspeitas nos termos de uso", "link": "https://en.wikipedia.org/wiki/Wire_(software)#Privacy_policy_changes"} %}. Por isso, eu recomendo evitar o Wire se possível.

### Email

<figure><img alt="Captura de tela do app de Android do Tutanota" height="600" src="/assets/2018-10-29_tutanota.png" /><figcaption>Tutanota</figcaption></figure>

**Use**: {% external_link {"text":"Protonmail", "link":"https://protonmail.com/"} %}, {% external_link {"text":"Tutanota", "link":"https://tutanota.com"} %}  
Evite: Gmail, Yahoo, Outlook

Assim como no caso de mensagens, queremos evitar que as mensagens estejam visíveis para a empresa que fornece o serviço. A única opção para isso são clientes de email que forneçam criptografia ponto-a-ponto, porque esses fazem seus emails serem criptografados no seu computador e somente o destinatário pode ver o email.

O Gmail tem umas funções que dão a impressão de que seus dados são criptografados, mas elas não são seguras.

As alternativas são {% external_link {"text":"Tutanota", "link":"https://tutanota.com"} %} ou {% external_link {"text":"Protonmail", "link":"https://protonmail.com/"} %}. Eu recomendo uma conta em cada um. Cada um implementa criptografia de uma maneira diferente e eles (ainda) não são compatíveis entre si. De modo que pra conseguir se comunicar com o máximo de gente possível de modo seguro, o ideal é ter uma conta em cada serviço. Pra quem ainda não usa o serviço, é possível enviar emails protegidos por senha, mas a senha tem que ser comunicada a quem vai receber de alguma forma segura.

### Compartilhamento de dados / Nuvem

**Use**: {% external_link {"text":"Nextcloud", "link":"https://nextcloud.com/"} %}  
Evite: Dropbox, iCloud, Google Drive, OneDrive

A grande maioria dos aplicativos de armazenamento de dados na nuvem não tem encriptação dos seus dados. O que quer dizer que os seus arquivos podem ser recuperados por terceiros, por falha de segurança ou funcionários mal intencionados.

Dropbox, iCloud, Google Drive, OneDrive, Box, todas essas soluções de armazenamento na nuvem tem acesso aos seus arquivos.

A recomendação aqui é o {% external_link {"text":"Nextcloud", "link":"https://nextcloud.com/"} %}. Além de ter código aberto, a partir da versão 14 possui uma opção para que os arquivos sejam criptografados localmente e enviados para o servidor criptografados. Ou seja, somente com a sua senha você pode ter acesso aos seus arquivos.

### Redes Sociais

Evite: usar redes sociais pra fins de organização de movimentos, coletivos e afins

Aqui cabe um grande parenteses: no geral, redes sociais devem ser consideradas como veículos públicos. Grupos de facebook são ótimos pra trocar histórias, mas devem ser evitados como método de organização de movimentos, coletivos e qualquer outro tipo de luta, nenhuma informação nesses grupos é realmente privada. O mesmo é válido pra outras redes sociais como Twitter, mesmo se a sua conta for fechada, isso quer dizer que os seus seguidores, _e os funcionários do Twitter_, podem ler suas mensagens.

Um outro problema: Twitter, Facebook e afins usam algoritmos desconhecidos para mostrar ou não os posts para outras pessoas. Isso faz com que eles decidam o que é relevante ou não para ser lido e pode fazer informações importantes serem escondidas por não serem detectadas como "importantes" pelos algoritmos.

Uma nota: se for excluir suas redes sociais, mude os seus perfis para algum país da união européia por alguns dias antes, de preferência usando uma VPN. As leis de proteção de dados da união européia mudaram bastante com o {% external_link {"text":"GDPR", "link":"https://pt.wikipedia.org/wiki/Regulamento_Geral_sobre_a_Prote%C3%A7%C3%A3o_de_Dados"} %} e é mais garantido que seus dados sejam realmente removidos se o seu perfil for reconhecido como sendo da UE. {% external_link {"text":"Vale notar que depois de alguns escândalos o Facebook promete que remover sua conta faz com que ela seja permanentemente removida", "link":"https://en.wikipedia.org/wiki/Criticism_of_Facebook#Inability_to_voluntarily_terminate_accounts"} %}.

Para substituir grupos de Facebook uma opção pode ser usar {% external_link {"text":"Matrix", "link":"http://matrix.org/"} %}, que permite a criação de grupos com criptografia inclusive para VoIP.
