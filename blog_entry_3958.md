--- IMPORTANTE ---
CMake Error: The source directory "C:/Libs/vcpkg/buildtrees/bitforge/src/bitforge-18.9.12" does not exist.
--- IMPORTANTE ---
```

Em segundo lugar, a cópia do header é feita tanto em release quanto em debug. A compilação via vcpkg irá te avisar que tem alguma coisa errada pois está duplicado, mas já há uma linha mágica que pode ser adicionada:

```
# Fix duplicated include
file(REMOVE_RECURSE ${CURRENT_PACKAGES_DIR}/debug/include)
```

O erro que deve acontecer na falta dessa mudança é o seguinte:

```
c:\Libs\vcpkg>vcpkg.exe build bitforge
-- Using cached C:/Libs/vcpkg/downloads/bitforge-18.9.12.zip
-- Configuring x86-windows
-- Building x86-windows-dbg
-- Building x86-windows-rel
-- Performing post-build validation
