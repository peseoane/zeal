# Foxtrot Zeal Docs
## Español / Spanish

> Este simple fork soluciona unos bugs del Zeal Docs original que impedían en determinados Docsets hacer búsquedas dado que el programa se cerraba.

**Versión release - No incluye símbolos de depuración**
> IMPORTANTE > Requiere Microsoft Visual C++ 2022, más abajo está la descarga, es recomendable bajar el fichero con instalador, lo hace automáticamente
<p align="center">
<img width="540" alt="ICON" src="https://github.com/peseoane/zeal/blob/master/ICON.png?raw=true">
</p>
### Fallos solucionados: 
- WebEngineSocket al generar una búsqueda bajo nuevos DOCSETS, hace un HALT general al programa. 
- Se cierra al hacer el query y no es usable con APIs modernas. https://github.com/zealdocs/zeal/issues/1339 - Solucionados problemas de escalado en pantallas HIDPI. 
- Mejorado rendimiento (1000 veces en consultas simples sin lógica booleana).

**¡Se puede buscar en la API de Java 18 sin que se cuelge!**
<p align="center">
![Screenshoot of Zeal not crashing](https://github.com/peseoane/zeal/blob/master/foto2.png?raw=true)
</p>

### Changelog: 
- Se ha migrado todo el código para ser compatible con x86_64. 
- Se ha migrado al Win10 SDK 10.0.22621 
- Se ha migrado a SQLite x64. 
- Se ha portado de Qt5 a Qt6. 
- Obsoleto qmake, se ha portado todo a cmake. 

## Compille Guide
[](https://github.com/peseoane/zeal/wiki/How-to-build-with-QT6-and-MSVC-2022)

## English UK

> This fork fixes some bugs in the original Zeal Docs that prevented certain Docsets from searching because the program would crash.

Release version - Does not include debug symbols

IMPORTANT > Requires Microsoft Visual C++ 2022, below is the download, it is recommended to download the file with installer, it does it automatically.

### Fixed bugs:

WebEngineSocket when generating a search under new DOCSETS, makes a general HALT to the program.
Closes on query and is not usable with modern APIs. zealdocs#1339 
- Fixed scaling issues on HIDPI screens. 
- Improved performance (1000x on simple queries without boolean logic).
- **Java 18 API can be searched without crashing!**
<p align="center">
![Screenshoot of Zeal not crashing](https://github.com/peseoane/zeal/blob/master/foto2.png?raw=true)
</p>
### Changelog:

- Migrated all code to be x86_64 compatible.
- Migrated to Win10 SDK 10.0.22621.
- Migrated to SQLite x64.
- Ported from Qt5 to Qt6.
- Obsolete qmake, everything has been ported to cmake.
