---
id: 814
title: Watching an array on idb eval window
date: 2012-02-13T14:59:31+00:00
author: Lond
layout: post
guid: /?p=814
permalink: /2012/02/13/watching-an-array-on-idb-eval-window/
tags:
  - array
  - debugger
  - Developments
  - dynamic allocated array
  - eval
  - evaluation
  - idb
  - intel
  - malloc
  - Nerdish
  - new
  - pointer
  - ponteiro
  - vetor
  - watch
---
Just to make sure the next person finds this easier than me, thanks to [printing an array in gdb](http://tuoq.blogspot.com/2008/06/printing-array-in-gdb.html "printing an array in gdb") I've been able to print one in idb, the intel debugger, as well. The syntax is the same as gdb.
```
* array @ size
```
size can be a variable.
