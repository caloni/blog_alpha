---------------------------------------------------------------------
pack_report: getpagesize()            =      65536
pack_report: core.packedGitWindowSize =   33554432
pack_report: core.packedGitLimit      =  268435456
pack_report: pack_used_ctr            =      22324
pack_report: pack_mmap_calls          =      10353
pack_report: pack_open_windows        =          4 /          6
pack_report: pack_mapped              =  101069594 /  163170978
---------------------------------------------------------------------
```

É óbvio que nem tudo serão mil maravilhas. Eu, por exemplo, encontrei um problema com case-sensitive que me deu algumas dores de cabeça:

```
fatal: Path Something/Resource.h not in branch
fast-import: dumping crash report to .git/fast_import_crash_676
bzr: broken pipe
```

O Git gera um arquivo de report onde estão as informações do ocorrido. Uma forma de contornar esse tipo de problema é primeiro exportar para um arquivo e editá-lo (corrigindo o case, por exemplo):

```
bzr fast-export --plain . > plain-export.txt
gvim fast-export.txt
hack hack hack
type fast-export.txt | git fast-import
```

_Note que talvez você precise de um editor que suporte arquivos gigantescos (como o Vim) e precise se debruçar sobre merges com arquivos com mesmo nome e diferentes cases. Isso que dá manter projetos com refactoring pesado._

Por fim, faça a conversão para todos os .bzr que tiver e haverá um .git com todo o histórico desses anos usando Bazaar. O próximo passo é montar o histórico de todos eles em apenas um repositório (se assim desejar). Segue uma série de comandos que pode ajudar para usar em uma batch:

```
@echo off
git remote add -f bzr ..\PathToOldConvertedRepo\%1
git merge bzr/master
git remote remove bzr
mkdir Archive\%1
echo Mova os arquivos importados
pause
git add --all
git ci -m "Archiving old Bazaar repo (%1)."
```

Você pode chamar um a um em cima de um repo novo:

```
mkdir NewRepo
cd NewRepo
git init
..\MyMergeBatch.bat OldRepoName
..\MyMergeBatch.bat OldRepoName2
..\MyMergeBatch.bat OldRepoName3
```

Para conseguir ter acesso ao histórico dos arquivos movidos, basta usar a opção -all do log:

```
git log --all -- MyRemovedPath
```

## Update

Tive alguns problemas em rastrear o histórico utilizando a estratégia de fazer merge no mesmo branch. A solução que encontrei, embora não exatamente direta, foi realizar os merges em branches apartados primeiro, mover os arquivos (de preferência, usando o git, para que ele detecte o rename), aplicar o commit e realizar o merge com o master. Há uma vantagem nessa estratégia, além do log --follow funcionar melhor: mantenha os branches originais, além do ponteiro para remote. Dessa forma, depois de alguns anos, saberá de onde veio esse merge maluco.

## Update2

Depois de um tempo testando essa técnica, descobri que o Git se perde novamente e não encontra mais todos os logs, mesmo com --follow  mesmo movendo os arquivos. O meu problema está relacionado com mesmos paths dos arquivos em repositórios diferentes. Paciência.

