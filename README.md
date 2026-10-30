# Raven Docs

Documentación comunitaria e independiente de **Raven 0.1.3**, la librería GUI en C11 del proyecto [oscar-soirey/Raven](https://github.com/oscar-soirey/Raven).

El sitio es estático y **no tiene dependencias externas**: HTML, CSS y JavaScript propios, imágenes locales y ninguna petición a CDN, fuentes remotas o servicios de analítica.

## Abrir el sitio

La forma más cómoda, con un servidor local:

```bash
cd raven-docs
python -m http.server 8000
```

Y abre <http://localhost:8000>.

También funciona haciendo doble clic en `index.html`: todo usa rutas relativas y los scripts se cargan desde el disco. Un servidor evita rarezas del navegador con `file://` y hace que la recarga en vivo del contenido sea más cómoda mientras editas la documentación.

## Páginas

| Archivo | Contenido |
|---|---|
| `index.html` | Portada: qué es Raven, características, galería y arranque rápido. |
| `guia.html` | Instalación con MinGW/CMake, primera ventana, bucle de frames, layout, ventanas, eventos, memoria, hilos, animaciones, diálogos, viewports, rendimiento y problemas frecuentes. |
| `xml.html` | Referencia del XML: reglas, ventana, atributos, slots, paneles, controles, herramientas, Markdown, tags propios, XMLC, recarga en vivo y documentos. |
| `interfaz.html` | Temas y estilos, materiales de cristal, blur, editor de código, docking, isla, herramientas de autor, accesibilidad, idiomas/RTL y `raven_web`. |
| `api.html` | La API pública por áreas y un índice completo de **921 funciones** con búsqueda instantánea. |
| `lenguajes.html` | Bindings de C++, Python, Rust, Go, C#, Zig y LuaJIT, XMLC en cada lenguaje, el IDE, los ejemplos y preguntas frecuentes. |

## Funciones del sitio

- **Búsqueda global** con `Ctrl+K` o `Cmd+K`: busca en los títulos y las entradas de todas las páginas y, en vivo, en las 921 funciones de la API.
- **Tema claro y oscuro** con preferencia guardada en `localStorage`.
- **Resaltado de sintaxis** propio para C, C++, Rust, Go, C#, Zig, Python, Lua, Bash, CMake, JSON, XML/HTML y CSV.
- **Botones de copiar** en todos los bloques de código.
- **Navegación lateral** con scrollspy y enlaces directos a cada sección.
- **Diseño responsive** con menú lateral desplegable en pantallas pequeñas.
- **Accesibilidad**: enlace para saltar al contenido, foco visible, `aria-label` en los controles y contraste cuidado en ambos temas.

## Estructura

```text
raven-docs/
├── index.html
├── guia.html
├── xml.html
├── interfaz.html
├── api.html
├── lenguajes.html
├── README.md
└── assets/
    ├── css/style.css
    ├── img/            capturas y logos
    └── js/
        ├── nav.js          árbol del menú lateral
        ├── site.js         tema, búsqueda, scrollspy, copiar y resaltado
        ├── search-index.js índice de títulos y entradas de las páginas
        └── api-index.js    921 funciones extraídas de los headers
```

## Regenerar los índices

`assets/js/api-index.js` se generó a partir de los headers públicos del paquete (`include/raven/*.h`). Cada entrada tiene la forma:

```js
{ n: "Rwindow_create", r: "Rid", a: "...", h: "Ventanas", f: "raven_window.h", d: "..." }
```

- `n`: nombre de la función.
- `r`: tipo de retorno.
- `a`: argumentos.
- `h`: área de la documentación.
- `f`: header donde se declara.
- `d`: descripción tomada del comentario del header.

`assets/js/search-index.js` se genera recorriendo los `h2[id]` y `h3[id]` de las seis páginas, con su primer párrafo. Tiene la forma:

```js
window.RAVEN_SEARCH = [{ t: "Instalación", page: "guia.html", hash: "instalacion", text: "..." }];
```

Si actualizas la librería, vuelve a generar ambos archivos para que la referencia y la búsqueda reflejen la nueva API. El sitio está pensado para leerse junto al paquete `raven-windows-mingw-x64-static` y su documentación original en `share/raven/`.

## Aviso

Raven está en desarrollo activo y su API pública puede cambiar antes de la versión 1.0. Esta documentación se escribió a partir del paquete **0.1.3** (headers, README y documentación incluida). No es documentación oficial del proyecto: es una guía comunitaria e independiente. Raven se distribuye bajo **Apache License 2.0**.
