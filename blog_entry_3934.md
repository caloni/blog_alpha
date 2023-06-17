------ Build started: Project: FixCMake, Configuration: Debug Win32 ------

Compiling...
FixCMake.cpp
Linking...

Build log was saved at "file://c:\Projects\samples\FixCMake\Debug\BuildLog.htm"
FixCMake - 0 error(s), 0 warning(s)

---------------------- Done ----------------------

    Build: 1 succeeded, 0 failed, 0 skipped

C:\Projects\samples\FixCMake>
```

Da mesma forma, projetos 2010+ devem usar o msbuild:

```
C:\Projects\samples\ConsoleApplication5>msbuild
Microsoft (R) Build Engine version 14.0.25420.1
Copyright (C) Microsoft Corporation. All rights reserved.

Building the projects in this solution one at a time. To enable parallel build, please add the "/m" switch.
Build started 9/18/2016 6:02:19 PM.
Project "C:\Projects\samples\ConsoleApplication5\ConsoleApplication5.sln" on node 1 (default targets).
ValidateSolutionConfiguration:
  Building solution configuration "Debug|x64".
The target "_ConvertPdbFiles" listed in a BeforeTargets attribute at "C:\Program Files (x86)\MSBuild\14.0\Microsoft.Common.targets\I
The target "_CollectPdbFiles" listed in an AfterTargets attribute at "C:\Program Files (x86)\MSBuild\14.0\Microsoft.Common.targets\I
The target "_CollectMdbFiles" listed in a BeforeTargets attribute at "C:\Program Files (x86)\MSBuild\14.0\Microsoft.Common.targets\I
The target "_CopyMdbFiles" listed in an AfterTargets attribute at "C:\Program Files (x86)\MSBuild\14.0\Microsoft.Common.targets\Impo
Project "C:\Projects\samples\ConsoleApplication5\ConsoleApplication5.sln" (1) is building "C:\Projects\samples\ConsoleApplication5\C
PrepareForBuild:
  Creating directory "x64\Debug\".
  Creating directory "x64\Debug\ConsoleA.C9D4BE8C.tlog\".
InitializeBuildStatus:
  Creating "x64\Debug\ConsoleA.C9D4BE8C.tlog\unsuccessfulbuild" because "AlwaysCreate" was specified.
ClCompile:
  C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\x86_amd64\CL.exe /c /ZI /nologo /W3 /WX- /sdl /Od /D _DEBUG /D _CONSOLE
  140.pdb" /Gd /TP /errorReport:queue stdafx.cpp
  stdafx.cpp
  C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\x86_amd64\CL.exe /c /ZI /nologo /W3 /WX- /sdl /Od /D _DEBUG /D _CONSOLE
  140.pdb" /Gd /TP /errorReport:queue ConsoleApplication5.cpp
  ConsoleApplication5.cpp
Link:
  C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\x86_amd64\link.exe /ERRORREPORT:QUEUE /OUT:"C:\Projects\samples\Console
  ib odbc32.lib odbccp32.lib /MANIFEST /MANIFESTUAC:"level='asInvoker' uiAccess='false'" /manifest:embed /DEBUG /PDB:"C:\Projects\sa
  cation5.lib" /MACHINE:X64 x64\Debug\ConsoleApplication5.obj
  x64\Debug\stdafx.obj
  ConsoleApplication5.vcxproj -> C:\Projects\samples\ConsoleApplication5\x64\Debug\ConsoleApplication5.exe
  ConsoleApplication5.vcxproj -> C:\Projects\samples\ConsoleApplication5\x64\Debug\ConsoleApplication5.pdb (Full PDB)
FinalizeBuildStatus:
  Deleting file "x64\Debug\ConsoleA.C9D4BE8C.tlog\unsuccessfulbuild".
  Touching "x64\Debug\ConsoleA.C9D4BE8C.tlog\ConsoleApplication5.lastbuildstate".
Done Building Project "C:\Projects\samples\ConsoleApplication5\ConsoleApplication5.vcxproj" (default targets).

Done Building Project "C:\Projects\samples\ConsoleApplication5\ConsoleApplication5.sln" (default targets).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:02.31

C:\Projects\samples\ConsoleApplication5>
```

### O que o Vim tem a ver com tudo isso?

Pois é. Tirando essa facilidade, as coisas no Vim para msbuild rodam particularmente bem. Basta alterarmos o makeprg da seguinte maneira:

```
:set makeprg=msbuild\ /nologo\ /v:q\ /property:GenerateFullPaths=true<CR>
```

As opções específicas são para gerar o path completo, as barras invertidas são por causa dessa mania do Vim de dar pau quando tem espaço em tudo.

A partir dessa configuração já é possível compilar um projeto estando em sua pasta:

{{< image src="GmIwJ19.png" caption="" >}}

Para o Visual Studio 2003 (ou qualquer um usando o devenv.com) é necessário mudar esse comando:

```
:set makeprg=devenv\ %\ /build\ Debug<CR>
```

Sim, temos que escolher uma configuração (o msbuild já escolhe por você). E note que ele usa o arquivo atual (%) para compilar. Isso quer dizer que isso irá exigir do usuário de Vim abrir o sln ou o vcproj e executar o :make a partir daí. De qualquer forma, ele funciona também:

{{< image src="PEr73NL.png" caption="" >}}

### Refinando a saída

Note que em nenhum dos casos erros conseguirão ser capturados para irmos direto no ponto do código-fonte onde ele está. Para isso funcionar, em nosso último passo, é necessário configurar o errorformat para que ele tenha um padrão que funcione com ambas as ferramentas. Depois de testar um pouco, cheguei nesse formato:

```
set errorformat=%f(%l)%m
```

Ele pega também os warnings, mas fazer o quê. Você não quer conviver com warnings em seu código pelo resto da vida, né? =)

VS2010:

{{< image src="4FymFj0.png" caption="" >}}

VS2003:

{{< image src="hXaP1X8.png" caption="" >}}

Note que depois de clicar em Enter ele pula para o primeiro erro da lista:

{{< image src="Xjbb5p3.png" caption="" >}}

E para navegar na lista é como o resultado de comandos como :vimgrep. :cnext e :cprevious vão para frente e para trás na lista, sempre pulando para o ponto no código onde está o erro.

### Dica final: convivendo com dois mundos

Como deu pra perceber, para conseguir usar o msbuild e o devenv ao mesmo tempo você seria obrigado a trocar o makeprg sempre que precisasse. Para facilitar seu uso, nada como fazer um mapeamento de atalhos:

```
map <F7> :set makeprg=devenv\ %\ /build\ Debug<CR>
map <S-F7> :set makeprg=msbuild\ /nologo\ /v:q\ /property:GenerateFullPaths=true<CR>
```

Para alguém curioso para ver minhas configurações do Vim (quem quiser compartilhar também, fique à vontade), [segue](https://github.com/Caloni/vim).

