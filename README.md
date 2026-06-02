# EcoMarket — Tienda virtual ecológica

Sitio web de una tienda en línea de productos ecológicos, reutilizables y de comercio justo. El proyecto se construyó usando exclusivamente **HTML5 y CSS3**, sin JavaScript, con un enfoque **mobile-first** y aprovechando pseudoclases modernas (`:has`, `:checked`, `:target`, `:focus-visible`) para resolver interacciones que normalmente requerirían scripting: filtrado del catálogo, sistema de favoritos persistente y filtrado del catálogo desde URL hash.

---

## Tabla de contenido

1. [Descripción del proyecto](#descripción-del-proyecto)
2. [Páginas del sitio](#páginas-del-sitio)
3. [Tecnologías y técnicas usadas](#tecnologías-y-técnicas-usadas)
4. [Estructura de carpetas](#estructura-de-carpetas)
5. [Cómo ejecutarlo localmente](#cómo-ejecutarlo-localmente)
6. [Decisiones de diseño](#decisiones-de-diseño)
7. [Compatibilidad de navegadores](#compatibilidad-de-navegadores)
8. [Autor](#autor)

---

## Descripción del proyecto

EcoMarket es la propuesta de una tienda online para productos sostenibles distribuidos en cuatro categorías: **Hogar**, **Moda**, **Cuidado Personal** y **Alimentos**. La idea fue construir un sitio de e-commerce completo, navegable y visualmente coherente, demostrando que se puede llegar lejos en términos de UX usando solo HTML semántico y CSS moderno.

El catálogo cuenta con veinte productos reales, cada uno con su categoría, rango de precio y disponibilidad. El usuario puede:

- Navegar por la página de inicio y descubrir productos destacados.
- Abrir el catálogo completo y filtrarlo por categoría, precio o disponibilidad (los grupos se combinan con AND).
- Hacer clic en "Ver más" desde la home para que el catálogo se abra ya filtrado por la categoría del producto.
- Marcar productos como favoritos (el estado persiste mientras la pestaña esté abierta).
- Conocer la historia de la marca en la sección "Sobre nosotros".
- Enviar un mensaje de contacto a través del formulario, con validación nativa del navegador.

---

## Páginas del sitio

### Inicio — `index.html`
Hero principal con llamada a la acción y una sección de **Productos destacados** con un producto representativo de cada categoría. Cada botón "Ver más" lleva al catálogo con el filtro de su categoría ya aplicado, y muestra un tooltip ("Ver todos los productos de Hogar", etc.) al pasar el mouse.

### Productos — `views/productos.html`
Catálogo completo con los veinte productos. Sidebar de filtros con tres grupos independientes:

- **Categorías**: Hogar, Moda, Cuidado Personal, Alimentos.
- **Rango de precio**: `$0–$20.000`, `$20.000–$50.000`, `$50.000–$100.000`, `$100.000–$200.000`.
- **Disponibilidad**: En stock, Agotado.

La lógica de cada grupo es: **sin selección significa mostrar todo**. Si no se marca ningún ítem dentro de un grupo, ese grupo no filtra nada. Si se marca uno o más, solo se muestran las cards que coincidan. Los tres grupos se combinan entre sí con AND. Cada card lleva una etiqueta de categoría con color identificador (sienna para Hogar, púrpura para Moda, teal para Cuidado Personal, ámbar para Alimentos) y un botón corazón para favoritos.

### Sobre nosotros — `views/sobre-nosotros.html`
Historia de la marca, principios sostenibles que la guían y testimonios de clientes.

### Contacto — `views/contacto.html`
Formulario de contacto con tres campos (nombre, correo, mensaje), todos con validación HTML5 nativa (`required`, `type="email"`, `minlength`). Incluye un mapa decorativo con pin, los datos de contacto físicos y enlaces a las redes sociales.

---

## Tecnologías y técnicas usadas

- **HTML5 semántico**: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `address`, jerarquía correcta de encabezados, `aria-label` donde aporta accesibilidad, `alt` en todas las imágenes.
- **CSS3 moderno** organizado en cuatro archivos por responsabilidad (ver [Estructura de carpetas](#estructura-de-carpetas)).
- **Variables CSS** (`--color-bg`, `--color-text`, `--color-btn-hvr`) para mantener consistencia y facilitar cambios de paleta.
- **Mobile-first** con dos breakpoints: `720px` (tablet) y `1024px` (desktop).
- **CSS Grid** para la cuadrícula de productos del catálogo y los layouts principales; **Flexbox** para los componentes internos (header de cards, formularios, lista de redes sociales).
- **Animaciones y transiciones** definidas en `css/animations.css` (`bigsmall`, `movingline`, `drawLine`, etc.).
- **Pseudoclases para lógica sin JavaScript**:
  - `:has()` para que un padre reaccione al estado de sus hijos.
  - `:checked` para los filtros del sidebar y para los corazones de favoritos.
  - `:target` para el filtro por URL hash desde "Ver más".
  - `:focus-visible` para outline accesible al navegar con teclado.
- **Validación nativa de formularios** con `required`, `type="email"`, `minlength`.
- **Favicon SVG** vectorial, escalable a cualquier tamaño sin pixelarse.

---

## Estructura de carpetas

```
EcoMarket_JhormanPenaloza/
├── index.html                  # Página de inicio
├── README.md                   # Esta documentación
├── views/
│   ├── productos.html          # Catálogo con filtros
│   ├── sobre-nosotros.html     # Historia, principios y testimonios
│   └── contacto.html           # Formulario, mapa y redes sociales
├── css/
│   ├── main.css                # Reset, variables, tipografía base, body
│   ├── layout.css              # Grids, layouts globales, breakpoints
│   ├── components.css          # Botones, cards, filtros, formularios, footer
│   └── animations.css          # Keyframes reutilizables
└── img/
    ├── hero/
    │   └── logo.png            # Logo principal de EcoMarket
    ├── products/
    │   └── producto1-20.{png,jpg}   # Imágenes del catálogo
    └── icons/
        ├── favicon.svg         # Favicon vectorial (hoja sobre fondo verde)
        ├── instagram.png       # Iconos monocromos de redes sociales
        ├── facebook.png
        ├── whatsapp.png
        └── x.png
```

---

## Cómo ejecutarlo localmente

El proyecto no tiene dependencias ni proceso de build. Tres formas de verlo:

**Opción 1 — Doble clic en `index.html`.** Funciona, aunque algunas rutas absolutas pueden no resolverse perfectamente al abrirse con el protocolo `file://`.

**Opción 2 — Live Server desde VS Code (recomendado).** Instalar la extensión [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer), abrir el proyecto en VS Code, hacer clic derecho sobre `index.html` y elegir "Open with Live Server". Se levanta un servidor local con recarga automática.

**Opción 3 — Servidor estático con Python.** En la raíz del proyecto:

```bash
python -m http.server 8000
```

Y luego abrir `http://localhost:8000` en el navegador.

---

## Decisiones de diseño

### Filtrado del catálogo sin JavaScript
La lógica "sin selección igual a mostrar todo" se implementa con la combinación `:has(.filter-X:checked):not(:has(#filter-Y:checked))`. En lenguaje natural: "si dentro de este grupo hay al menos uno marcado, pero ESTE específico no lo está, oculta las cards de su tipo". Cuando no hay ningún checkbox marcado en el grupo, la primera condición falla y el filtro no aplica. Es la misma lógica que usan los filtros de Amazon o Mercado Libre.

### Filtrado desde URL al venir de "Ver más"
Dentro de `<main class="catalog">` hay cuatro anchors invisibles (`<span id="cat-hogar">`, etc.). Cuando la URL trae el hash correspondiente, `:target` activa ese span, `:has()` propaga la condición al `.catalog` y se ocultan las cards que no coinciden con la categoría. El filtro por URL se desactiva automáticamente en cuanto el usuario marca cualquier checkbox del sidebar, para que la interacción se sienta natural.

### Favoritos persistentes
Cada corazón es un `<label class="card-fav">` que envuelve un `<input type="checkbox">` invisible. Hacer clic en el label togglea el checkbox, `:has(.card-fav-toggle:checked)` activa el estilo de "favoriteado" y dispara la animación `bigsmall`. La técnica permite marcar tantos favoritos como se quiera, no requiere IDs únicos por card y no contamina la URL con un `#prod-N` que provocaría scroll-jumps.

### Mobile-first con dos breakpoints
Los estilos base están escritos para pantallas pequeñas (idealmente 360-720px). El primer breakpoint en `720px` adapta tipografías y comienza a usar columnas más anchas; el segundo en `1024px` activa los layouts de escritorio definitivos (grid de cuatro columnas en el catálogo, sidebar de filtros sticky, hero a pantalla completa, etc.).

### Paleta de categorías
Cada categoría tiene un color identificador elegido por afinidad semántica con lo que representa: sienna (#a0522d) para Hogar (madera y cerámica), plum (#7e3a8a) para Moda (textiles y elegancia), teal (#0d9488) para Cuidado Personal (frescura y limpieza), ámbar (#c2410c) para Alimentos (calidez y apetito). Todos los colores tienen contraste suficiente con texto blanco para etiquetas legibles.

### Iconografía
El **favicon** es un SVG: una hoja blanca diagonal con nervaduras sobre un cuadrado redondeado verde marca. Al ser vectorial, se ve nítido en cualquier tamaño (16, 32, 64, 256 px) sin necesidad de mantener múltiples archivos PNG.

Los **iconos de redes sociales** son PNG monocromos. En los footers (fondo oscuro) se invierten a blanco con `filter: invert(1)`; en la sección de contacto (fondo blanco) van tal cual y se invierten solo en hover, cuando el fondo del botón pasa a verde.

---

## Compatibilidad de navegadores

El sitio depende de `:has()`, que está soportado de forma estable desde:

- Chrome / Edge 105 (agosto 2022)
- Safari 15.4 (marzo 2022)
- Firefox 121 (diciembre 2023)

En navegadores anteriores los filtros y el toggle de favoritos pierden funcionalidad, pero el resto del sitio (navegación, lectura, formulario) sigue siendo plenamente accesible.

---

## Autor

**Jhorman Peñaloza** — [@JopsWtD](https://github.com/JopsWtD)

Proyecto desarrollado como parte del curso de Desarrollo Web (HTML + CSS).
