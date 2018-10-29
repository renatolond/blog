---
id: 848
title: 'Raspberry Pi: Torrents e séries'
date: 2012-11-19T08:08:42+00:00
author: Lond
layout: post
guid: /?p=848
permalink: /2012/11/19/raspberry-pi-torrents-e-series/
tags:
  - Azureus
  - Debian
  - Feed
  - Feeds
  - Flexget
  - kTorrent
  - Linux
  - Linux
  - Nerdish
  - R-Pi
  - Raspberry Pi
  - Raspbmc
  - RPi
  - RSS
  - rTorrent
  - Séries
  - Torrent
  - Torrents
  - Transmission
  - TV Show
  - TV Shows
  - Ubuntu
  - uTorrent
  - Vuze
  - XBMC
---

_**Atualização em 2018**_: desde que eu escrevi esse post, melhores opções apareceram pra automatizar essa tarefa. Dentre elas eu recomendo dar uma olhada no [SickChill](http://sickchill.github.io) e no [CouchPotato](https://couchpota.to/). Eles substituem o flexget com muito mais funções (como por exemplo, fazer o download de legendas).

Por isso, esse post está basicamente desatualizado e está aqui só pra fins históricos. :)

---

No <a title="Raspberry Pi: O Media Center de US$35" href="/2012/11/16/raspberry-pi-o-media-center-de-us35/">último post</a> eu comentei um pouco sobre o raspberry e sobre o XBMC, mas a outra coisa que precisa é botar os filmes e séries dentro dele, e ficar passando manualmente quebra um pouco o propósito de ter o negócio todo contido numa caixa só.

Como ele roda Linux, tem duas opções principais: Transmission e rTorrent.

Nunca havia usado nenhum dos dois, mas a maioria das dicas nos fóruns fala do transmission e foi o que acabei escolhendo.

**_Nota_**: Confira duas vezes ao copiar os comandos porque pode ser que alguns caracteres estejam incorretos

Instalar ele é a parte fácil, assumindo que você esteja num raspbmc, basta abrir um ssh pro raspberry e fazer

```
apt-get install transmission-daemon
```

Com isso feito, pra iniciar basta fazer:

```
sudo /etc/init.d/transmission-daemon start
```

O Raspberry não tem o hardware mais poderoso do mundo, então é bom colocar algumas limitações nas configurações do transmission, as minhas são as seguintes:

_**Update (20-11-2012, 14:12)**_: Todas as configurações do transmission ficam em `/etc/transmission-daemon/settings.json`

```
"download-queue-enabled": true,
"download-queue-size": 1,
"peer-limit-global": 240,
"peer-limit-per-torrent": 100,
"seed-queue-enabled": true,
"seed-queue-size": 9,
"speed-limit-up": 20,
"speed-limit-up-enabled": true
```

É uma boa também mudar o local de download dos arquivos. Coloquei duas pastas separadas, como o transmission permite, ficou assim (Raspberry Pi é o meu hd externo):

```
"download-dir": "/media/Raspberry Pi/seeding",
"incomplete-dir": "/media/Raspberry Pi/downloading",
"incomplete-dir-enabled": true,
```

Não esqueça que o transmission tem que ter permissão para escrever nessas pastas. Com essas configurações e ligando o rpc, já dá pra acessar o transmission e mandar ele baixar coisas pela interface web (Não esqueça de botar seu próprio nome de usuário e password):

```
"rpc-authentication-required": true,
"rpc-bind-address": "0.0.0.0",
"rpc-enabled": true,
"rpc-password": "**_seu-password_**",
"rpc-port": 9091,
"rpc-url": "/transmission/",
"rpc-username": "**_seu-usuário_**",
"rpc-whitelist": "127.0.0.1,192.168.\*.\*",
"rpc-whitelist-enabled": true,
```

Mas não vamos ficar contentes só com isso. A boa é que quando saiam séries novas, elas sejam baixadas automagicamente. Pra isso, vamos instalar o flexget:

```
easy_install flexget
easy_install transmissionrpc
```

A configuração, que deve ficar em `~/.flexget/config.yml` deve ficar parecida com essa:

[Config.yml no paste.bin](http://pastebin.com/wqhLg6cY "config.yml")

Com essa configuração, ele vai baixar somente com definição de 720p, e que tenha qualidade de hdtv ou mais (dvdrip, etc).

É preciso ajustar as configurações do plugin do transmission para as mesmas usadas no rpc.

Daí basta ir nas configurações do raspbmc, pela interface do XBMC mesmo, e lá ligar o cron. Com ele ligado, basta adicionar a seguinte linha ao crontab (crontab -e):

```
0 \* \* \* \* /usr/local/bin/flexget --cron
```

Isso vai fazer com que o flexget seja chamado uma vez por hora, botando suas séries no transmission e tal :)

Ainda pretendo fazer a última parte da automatização: pegar as séries que foram baixadas e movê-las para a pasta correta e reindexar o xbmc, e já baixar as legendas. Já comecei fazendo isso tirando os que já estão com seeding completos para uma pasta separada, a partir da dica <a title="How to Automatically Move and Remove Transmission-Daemon Downloads" href="http://1000umbrellas.com/2010/04/28/how-to-automatically-move-and-remove-transmission-daemon-downloads" target="_blank">desse post</a>. Se for usar, note que só consegui usar esse script modificando as chamadas do transmission para incluir `--auth <seu-usuário>:<seu-password>`

Uma segunda coisa ideal seria que as séries tivessem uma prioridade alta quando adicionadas no transmission, parando qualquer torrent que existisse para que elas fossem baixadas. Mas isso é assunto para outra vez ;)

**Bônus**: Tudo aqui deve funcionar para qualquer distro, com as devidas adaptações :)
