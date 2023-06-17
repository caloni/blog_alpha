------ Build started: Project: MyFirstLib, Configuration: Debug Win32 ------
Compiling...
mymath.c
Creating library...
Build log was saved at "file://c:\Projects\temp\MyFirstLib\Debug\BuildLog.htm"
MyFirstLib - 0 error(s), 0 warning(s)
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

Para usar uma LIB temos inúmeras maneiras de fazê-lo. A mais simples que eu conheço é criar um novo projeto no mesmo Solution de sua LIB. Um console, por exemplo:

{{< image src="myfirstlib4.png" caption="MyFirstLib4" >}}

{{< image src="myfirstlib5.png" caption="MyFirstLib5" >}}

{{< image src="myfirstlib6.png" caption="MyFirstLib6" >}}

Se você seguiu todos os passos direitinho, e eu estou assumindo que você já sabia como criar um projeto console, sua saída da compilação talvez seja mais ou menos essa:

```
------ Build started: Project: MyFirstCmd, Configuration: Debug Win32 ------
Compiling...
mycmd.c
Linking...
mycmd.obj : error LNK2019: unresolved external symbol mult referenced in function main
mycmd.obj : error LNK2019: unresolved external symbol sum referenced in function main
c:\Projects\temp\MyFirstLib\Debug\MyFirstCmd.exe : fatal error LNK1120: 2 unresolved externals
Build log was saved at "file://c:\Projects\temp\MyFirstCmd\Debug\BuildLog.htm"
MyFirstCmd - 3 error(s), 0 warning(s)
========== Build: 0 succeeded, 1 failed, 1 up-to-date, 0 skipped ==========
```

Dois erros! Ele não achou os símbolos mult e sum. Mas eles estão logo ali! E agora?

Nada a temer: tudo que temos que fazer é falar para o Solution que o projeto myfirstcmd depende do projeto myfirstlib:

{{< image src="myfirstlib7.png" caption="MyFirstLib7" >}}

{{< image src="myfirstlib8.png" caption="MyFirstLib8" >}}

```
