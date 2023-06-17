---
categories: []
date: '2016-09-18'
tags: null
title: Usando GVim com projetos do Visual Studio
---

A vida dos programadores C/C++ Windows -- e que geralmente precisam do Visual Studio -- está um abandono total. A configuração de make dos projetos sempre foi baseada no uso de makefiles, assim como no Unix, e por isso mesmo o uso da ferramenta nmake do SDK do Windows era a maneira padrão de se compilar e ver o resultado de dentro do Vim para projetos Windows. Com o advento do .NET, do Visual Studio 2003 e dos XMLs disfarçados como arquivos de projeto e solution, o uso do makefile foi paulatinamente abandonado, gerando diferentes versões de ferramentas -- todas incompatíveis -- para conseguir compilar um ou mais cpps e conseguir ver o resultado.

Por isso mesmo é um assunto pouco explorado nos fóruns do Stack Overflow como configurar decentemente o comando :make do Vim para conseguir realizar o ciclor program-compile-debug que já era feito desde a época do Amiga OS (e conhecido no manual do Vim como Quickfix). Ninguém se dá ao trabalho de usar esse modelo torto.

Houve um tempo que eu mesmo pesquisei algumas soluções, e caí no velho problema de tentar conviver com diferentes versões do Visual Studio. Deixei de lado o Vim por uns anos, e passei a usar o VsVim, um plugin que roda em várias versões do Visual Studio e utiliza o vimrc de sua instalação.

Hoje voltei a fuçar esse problema e depois de algumas horas tentando entender qual a dinâmica que deve ser seguida, cheguei a dois usos legítimos do make no Visual Studio: o modo legado, através do devenv, e o modo comportado, que usa a ferramenta MsBuild para encontrar o projeto e a solution que devem ser compilados.

### Colocando as coisas no path

A não ser que você coloque o path das ferramentas direto nos comandos (algo que não recomendo pois as coisas no Vim começam a ficar estranhas com paths com espaços, algo abundante no Windows) é preferível que você escolha qual devenv e qual msbuild deseja utilizar e definir isso na variável de sistema path. No meu exemplo estou usando o msbuild para qualquer Visual Studio acima do 2010 (como o 2015), pois já está padronizado, e como tenho projetos no VS2003 para manter, escolhi deixar o devenv.com com ele.

```
set path=%path%;C:\Program Files (x86)\MSBuild\14.0\Bin
set path=%path%;c:\Program Files (x86)\Microsoft Visual Studio .NET 2003\Common7\IDE
```

Note que essa configuração, para ficar persistente, precisa ser definida através do Painel de Controle ou Propriedades do Sistema. Google for it.

Depois de configurado, qualquer projeto deve ser compilável em 2003 pela linha de comando (através do devenv.com):

```
C:\Projects\samples\FixCMake>devenv.com FixCMake.sln /build Debug

Microsoft (R) Development Environment  Version 7.10.3077.
Copyright (C) Microsoft Corp 1984-2001. All rights reserved.
