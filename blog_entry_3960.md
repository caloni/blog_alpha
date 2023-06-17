--- IMPORTANTE ---
The software license must be available at ${CURRENT_PACKAGES_DIR}/share/bitforge/copyright
--- IMPORTANTE ---

    file(COPY ${CURRENT_BUILDTREES_DIR}/src/bitforge/LICENSE DESTINATION ${CURRENT_PACKAGES_DIR}/share/bitforge)
    file(RENAME ${CURRENT_PACKAGES_DIR}/share/bitforge/LICENSE ${CURRENT_PACKAGES_DIR}/share/bitforge/copyright)
Found 1 error(s). Please correct the portfile:
    c:\Libs\vcpkg\ports\bitforge\portfile.cmake
-- Performing post-build validation done
Elapsed time for package bitforge:x86-windows: 4.188 s
Error: Building package bitforge:x86-windows failed with: POST_BUILD_CHECKS_FAILED
Please ensure you're using the latest portfiles with `.\vcpkg update`, then
submit an issue at https://github.com/Microsoft/vcpkg/issues including:
  Package: bitforge:x86-windows
  Vcpkg version: 0.0.113-nohash

Additionally, attach any relevant sections from the log files above.
```

Basicamente isso é o que você precisa para começar a construir seu pacote:

```
c:\Libs\vcpkg>vcpkg.exe build bitforge
-- Using cached C:/Libs/vcpkg/downloads/bitforge-18.9.12.zip
-- Configuring x86-windows
-- Building x86-windows-dbg
-- Building x86-windows-rel
-- Installing: C:/Libs/vcpkg/packages/bitforge_x86-windows/share/bitforge/copyright
-- Performing post-build validation
-- Performing post-build validation done
Elapsed time for package bitforge:x86-windows: 4.224 s
```

O próximo passo é instalar:

```
c:\Libs\vcpkg>vcpkg.exe install bitforge
The following packages will be built and installed:
    bitforge[core]:x86-windows
Starting package 1/1: bitforge:x86-windows
Building package bitforge[core]:x86-windows...
-- Using cached C:/Libs/vcpkg/downloads/bitforge-18.9.12.zip
-- Configuring x86-windows
-- Building x86-windows-dbg
-- Building x86-windows-rel
-- Installing: C:/Libs/vcpkg/packages/bitforge_x86-windows/share/bitforge/copyright
-- Performing post-build validation
-- Performing post-build validation done
Building package bitforge[core]:x86-windows... done
Installing package bitforge[core]:x86-windows...
Installing package bitforge[core]:x86-windows... done
Elapsed time for package bitforge:x86-windows: 4.239 s

Total elapsed time: 4.239 s

c:\Libs\vcpkg>dir /s /b installed\x86-windows\bitforge.*
c:\Libs\vcpkg\installed\x86-windows\debug\lib\bitforge.lib
c:\Libs\vcpkg\installed\x86-windows\include\bitforge.h
c:\Libs\vcpkg\installed\x86-windows\lib\bitforge.lib
c:\Libs\vcpkg\installed\x86-windows\share\bitforge
```

E voilá! Agora o include está disponível, as funções estão disponíveis, o link está funcionando e seu pacote pode ser compartilhado com toda a empresa. Basta copiar a pasta ports/bitforge ou adicioná-la no repositório por um commit.

{{< image src="XeeD4Se.png" caption="" >}}

[parseamento de argumentos]: {{< relref "getarg" >}}

