---
id: 830
title: 'Raspberry Pi: O Media Center de US$35'
date: 2012-11-16T15:24:58+00:00
author: Lond
layout: post
guid: /?p=830
permalink: /2012/11/16/raspberry-pi-o-media-center-de-us35/
tags:
  - Arm
  - Gadgets
  - HDMI-CEC
  - Linux
  - Nerdish
  - Pibow
  - R-Pi
  - Raspberry Pi
  - Raspbmc
  - RPi
  - XBMC
---
Talvez você tenha ouvido falar do Raspberri Pi, a idéia original era fazer um computador para construir um computador pequeno e barato pra ensinar crianças a programar. A história está bem explicada no about do site dos caras, mas basicamente a idéia é que antes existiam Commodore 64 e outros pra fazer muleques aprenderem a programar no (grande) tempo vago que toda criança tem e hoje em dia não existe um computador para esse fim.

Só que quando os caras começaram a divulgar os specs finais da parada, ficou claro que ele ia ser um computador razoavelmente poderoso por US$35. Claro que foi um pequeno frenesi entre todos os hobbyistas da internet.

As specs finais ficaram assim para o modelo B, que é o que é mais interessante:

> Um processador ARM11 com 700Mhz
>
> Uma Broadcom VideoCore IV, que suporta OpenGL ES 2.0 e 1080p30 (isso é, até 30 frames por segundo).
>
> 256Mb de ram compartilhada com a GPU.
>
> 2 portas USB
>
> Saída HDMI e RCA para vídeo, além de uma saída de áudio 3.5mm.
>
> Uma entrada para SD
>
> Ethernet 10/100

Demorei pra escrever esse artigo, e nesse meio do caminho já até decidiram aumentar pra 512MB a memória do Raspberry, mas demorei porque queria amaciar mais o negócio, testar mais e saber das limitações, antes de falar bem ou mal dele.

A coisa toda é alimentada por qualquer transformador que entregue 5V a 700mA. Eu estou segurando por enquanto com meu carregador do celular.

Parece bom demais pra ser verdade? Pois é, como eu disse, um computador para hobbyistas, né? Porque ele vem assim, pelado. Só uma plaquinha sem case, sem nada.

<figure>
  <a href="http://instagram.com/p/OaNxZgyf77/"><img class=" " title="O meu Raspberri Pi funcionando" src="https://scontent-bru2-1.cdninstagram.com/vp/42c750020248b522674a9563a0849243/5B5D59EC/t51.2885-15/e15/11189219_358774464326592_1626318169_n.jpg" alt="Um Raspberri Pi ligado" width="367" height="367" /></a>
  <figcaption>O meu Raspberri Pi funcionando</figcaption>
</figure>

Mas nem tudo está perdido. Existem algumas cases já pra ele, tipo o [Pibow](http://www.pibow.com/), ou mesmo <a title="9 amazing Raspberry Pi case mods (including one that looks like a raspberry!)" href="http://venturebeat.com/2012/07/16/9-amazing-raspberry-pi-case-mods-including-one-that-looks-like-a-raspberry/" target="_blank">uma dessas nove citadas nesse artigo</a>. E enquanto a case num chega, dá pra improvisar umas de papel, que podem ser encontradas no fórum. As melhores, na minha opinião, são <a title="Raspberry Pi &quot;Oven Window&quot; Case" href="http://www.bizypromotions.co.uk/rpicase.html" target="_blank">essa</a> e <a title="The Punnet – a card case for you to print (for free)" href="http://www.raspberrypi.org/archives/1310" target="_blank">essa</a>.

<figure>
<a href="http://instagram.com/p/Q4pJSNyf_6/"><img class=" " title="Meu Raspberry Pi no Pibow" src="https://scontent-bru2-1.cdninstagram.com/vp/50be079cd29dec9036a6a0cbbb67605d/5B6F52C3/t51.2885-15/e15/11241336_1440884002888924_678722125_n.jpg" alt="Meu Raspberry Pi no Pibow" width="367" height="367" /></a>
<figcaption>Meu Raspberry Pi no Pibow</figcaption>
</figure>

Pra quem não conhece, existe um media center muito bom, chamado XBMC. O XBMC foi criado com intuito de de ser um media center pro Xbox original, mas hoje em dia funciona em diversos dispositivos, incluindo Windows, Linux, Mac OS e recentemente Android e iOS.

Rapidamente fizeram um port do XBMC para o Raspberry Pi e agora tem uma distribuição chamada Raspbmc, que inicia direto no XBMC e deixa tudo pronto para o uso do media center.

<figure>
<a href="http://imgur.com/7dipQ"><img title="O Raspbmc, a distro que faz com que o XBMC abra na sua TV." src="http://www.howtogeek.com/wp-content/uploads/2012/07/2012-07-24_155042.jpg" alt="O Raspbmc, a distro que faz com que o XBMC abra na sua TV." width="390" height="184" /></a>
<figcaption>O Raspbmc, a distro que faz com que o XBMC abra na sua TV.</figcaption>
</figure>

Como media center o Raspberry Pi é bem decente. Tenho visto arquivos em 720p sem problemas, a vantagem do XBMC é que ele tem um plugin de legendas que baixa a partir de grande sites, como opensubtitles e legendas.tv

É preciso lembrar, no entanto, que o raspberry só tem um ARM, que funciona normalmente a 700mhz, então não espere velocidades incríveis. Multitarefa normalmente exige muito dele, já que o XBMC não é o software mais otimizado o possível. Ou seja: NÃO é um hardware para quem quer um media center e não ligar pra mais nada. É pra quem tem paciência de parar pra configurar e debugar coisas.

Ainda há muitas coisas que não estão funcionando tão bem, esses dias descobri que colocar o sistema no hd externo, pela usb, parece dar um desempenho muito superior ao SD Card. A culpa provavelmente está no SD, que não deve ser dos mais rápidos.

Outros problemas comuns são com relação a fonte de energia. O Raspberry não tem uma fonte padrão, recomendada. O que se recomenda é que se use uma fonte qualquer, que tenha 5V de saída a pelo menos 0.7A. A do meu celular, 5V e 1A, anda segurando muito bem, mesmo em situações de muita carga no sistema. Mas pra garantir, meu hd externo tem fonte própria de força.

Ainda tenho algumas coisas pra fazer com que o Raspberry vire meu media center perfeito, mas do jeito que ele está hoje, está muito legal. Mantenho ele ligado 24/7, já tenho uma quantidade grande de filmes nele e um hd de 1TB, ou seja, vai dar pra deixar bastante coisa por lá. Fica aí a dica, mesmo que não seja um Raspberry Pi, pegue um media center pra deixar na sua TV. É ótimo!

**Update 1 (16/11/12, 16:36)**: Esqueci de um detalhe muito importante!
  
O raspbmc suporta um protocolo, HDMI-CEC, que permite que o controle remoto de TVs que o suportam seja usado diretamente no XBMC, ou seja, nada de mouse ou teclado externo. Fica parecendo que o XBMC é um recurso da própria TV, super prático :)
