--- IMPORTANTE ---
Include files should not be duplicated into the /debug/include directory. If this cannot be disabled in the project cmake, use
    file(REMOVE_RECURSE ${CURRENT_PACKAGES_DIR}/debug/include)
--- IMPORTANTE ---
The software license must be available at ${CURRENT_PACKAGES_DIR}/share/bitforge/copyright

    file(COPY ${CURRENT_BUILDTREES_DIR}/src/bitforge/LICENSE DESTINATION ${CURRENT_PACKAGES_DIR}/share/bitforge)
    file(RENAME ${CURRENT_PACKAGES_DIR}/share/bitforge/LICENSE ${CURRENT_PACKAGES_DIR}/share/bitforge/copyright)
Found 2 error(s). Please correct the portfile:
    c:\Libs\vcpkg\ports\bitforge\portfile.cmake
-- Performing post-build validation done
Elapsed time for package bitforge:x86-windows: 4.139 s
Error: Building package bitforge:x86-windows failed with: POST_BUILD_CHECKS_FAILED
Please ensure you're using the latest portfiles with `.\vcpkg update`, then
submit an issue at https://github.com/Microsoft/vcpkg/issues including:
  Package: bitforge:x86-windows
  Vcpkg version: 0.0.113-nohash

Additionally, attach any relevant sections from the log files above.
```

E por último, é obrigatório ter um arquivo de copyright, no caso o nosso LICENSE do projeto. O portfile.cmake já tem o comando, mas está comentado:

```
# Handle copyright
file(INSTALL ${SOURCE_PATH}/LICENSE DESTINATION ${CURRENT_PACKAGES_DIR}/share/bitforge RENAME copyright)
```

O erro que deve acontecer na falta dessa mudança é o seguinte:

```
c:\Libs\vcpkg>vcpkg.exe build bitforge
Your feedback is important to improve Vcpkg! Please take 3 minutes to complete our survey by running: vcpkg contact --survey
-- Using cached C:/Libs/vcpkg/downloads/bitforge-18.9.12.zip
-- Configuring x86-windows
-- Building x86-windows-dbg
-- Building x86-windows-rel
-- Performing post-build validation
