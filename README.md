# EcoMarket - Tienda de Productos Ecológicos y Sustentables

Sitio web multipágina desarrollado con **HTML5 semántico** y **CSS3 modular puro** (sin librerías externas), diseñado bajo un enfoque **Mobile First**, metodologías de diseño responsivo y restricciones estrictas de **cero JavaScript** para optimizar el rendimiento de carga y la eficiencia técnica.

---

## 1. Descripción del Negocio

**EcoMarket** es una tienda en línea dedicada exclusivamente a productos ecológicos, reutilizables y sustentables. Su objetivo es ofrecer una plataforma accesible y atractiva donde los usuarios puedan explorar alternativas 100% ecológicas, conocer los principios de sostenibilidad de la marca y realizar compras responsables. El proyecto está diseñado para transmitir frescura, transparencia y calma mediante interfaces de usuario limpias y naturales.

---

## 2. Estructura Semántica y Arquitectura del Sitio

El proyecto consta de una página principal y tres vistas secundarias interconectadas que comparten una cabecera global y un pie de página estandarizado:

- **`index.html` (Página Principal / Home):** Presentación de la plataforma mediante un banner principal (*Hero*), grid de productos destacados, llamadas a la acción y pie de página corporativo.
- **`views/productos.html` (Catálogo):** Vitrina completa con un buscador visual superior, sidebar de filtros lateral (*sticky*), grid adaptativo de 20 productos con etiquetas de stock y botones interactivos de favoritos.
- **`views/sobre-nosotros.html` (Brand Story):** Sección de historia corporativa en diseño *Flexbox*, grid de principios ecológicos con iconos SVG personalizados y un carrusel de testimonios interactivo.
- **`views/contacto.html` (Contacto):** Formulario inteligente con validación visual nativa en tiempo real (`:valid` / `:invalid`), mapa de ubicación estático estilizado y accesos a redes sociales con animaciones de escala.

### Justificación de Etiquetas Semánticas HTML5

- **`<header>` y `<nav>`:** Definen el encabezado institucional y la barra de navegación principal con soporte responsivo mediante un patrón de selector `checkbox` en CSS puro.
- **`<main>`:** Delimita el contenido central y exclusivo de cada vista, garantizando una correcta jerarquía de títulos.
- **`<section>` y `<article>`:** Organizan lógicamente los bloques temáticos independientes, tales como las tarjetas individuales de productos, principios ecológicos y testimonios de clientes.
- **`<aside>`:** Implementado en la vista de catálogo para albergar la barra lateral fija de filtros (*sticky*).
- **`<footer>`:** Pie de página estructurado con información institucional, enlaces legales y accesos directos a redes sociales.

---

## 3. Identidad Visual y Variables CSS (`:root`)

La paleta cromática se diseñó con base en tonos naturales institucionales (verdes orgánicos y tonos tierra/beige), centralizados mediante **variables CSS** dentro del selector `:root` para asegurar mantenibilidad y consistencia visual:

| Variable | Valor | Aplicación |
| :--- | :--- | :--- |
| `--color-primary` | `#2ecc71` | Tono verde base para botones principales y acentos |
| `--color-primary-dark` | `#27ae60` | Tono verde oscuro para estados interactivos y precios |
| `--color-earth` | `#f5f5dc` | Fondo secundario cálido tipo tierra/beige |
| `--color-earth-light` | `#fafaf0` | Fondo general suave de la página |
| `--color-white` | `#ffffff` | Superficie de tarjetas, contenedores y cabecera |
| `--color-text` | `#2c3e50` | Color primario de texto y títulos |
| `--color-text-muted` | `#596a7a` | Descripciones secundarias y notas |
| `--color-border` | `#dce4ec` | Bordes sutiles para inputs y tarjetas |
| `--color-error` | `#e74c3c` | Indicadores de agotado y validación de errores en formularios |
| `--color-success` | `#27ae60` | Indicadores de stock y validación exitosa de formularios |

---

## 4. Arquitectura CSS Modular

Para mantener un código limpio y escalable, los estilos se dividieron en 4 hojas de estilo independientes vinculadas en el orden correcto:

1. **`css/main.css`:** Contiene el reset universal de caja, la definición de variables globales (`:root`) y las reglas tipográficas base.
2. **`css/layout.css`:** Define los contenedores globales, el encabezado fijo (*sticky*), el pie de página y los sistemas de diseño estructurados mediante **CSS Grid** y **Flexbox** adaptados para *Mobile First*.
3. **`css/components.css`:** Agrupa los componentes visuales reutilizables, incluyendo tarjetas de productos (`.product-card`), botones, barra de búsqueda, sidebar de filtros, paginación, carrusel y estados interactivos de formularios y favoritos.
4. **`css/animations.css`:** Contiene las transiciones globales suaves, keyframes de aparición (*fadeInUp*), efectos de elevación en tarjetas y animaciones de escala al pasar el cursor sobre los iconos sociales.

---

## 5. Interactividad en CSS Puro (Cero JavaScript)

Cumpliendo con la restricción técnica de ausencia de scripts, toda la interactividad del sitio se resolvió aprovechando las capacidades avanzadas de CSS3:

- **Menú de navegación hamburguesa móvil:** Implementado mediante un selector tipo `checkbox` oculto (`#nav-toggle`) combinado con el selector de hermanos generales (`~`) para desplegar y colapsar el menú dinámicamente sin requerir eventos en JavaScript.
- **Gestión de favoritos interactivos:** Cada tarjeta de producto incluye un control de selección (`checkbox` o enlaces con anclas) que cambia el color del icono de corazón a un tono rojo de alerta y aplica zoom visual utilizando pseudo-clases como `:active`, `:target` o `:checked + .btn-fav`.
- **Validación visual inteligente en formularios:** Los campos del formulario de contacto aprovechan las pseudo-clases nativas `:valid` y `:invalid` para cambiar dinámicamente el color de los bordes del input (rojo en caso de datos incorrectos/incompletos y verde con fondo claro al cumplirse los criterios de longitud y formato).
- **Carrusel de testimonios responsivo:** Diseñado mediante contenedores con `overflow-x: auto` y la propiedad `scroll-snap-type: x mandatory`, permitiendo un desplazamiento fluido por bloques en dispositivos táctiles y de escritorio.

---

## Dificultades Técnicas y Soluciones Implementadas

Durante el desarrollo del proyecto se superaron diversos retos propios de la maquetación avanzada sin frameworks ni scripts:

### 1. Despliegue del menú móvil sin soporte de JavaScript
- **Problema:** En pantallas estrechas, el menú de navegación principal ocupaba espacio valioso y no existía un mecanismo tradicional en CSS para alternar su visibilidad sin manipular el DOM mediante eventos de clic.
- **Causa:** Las propiedades de visualización tradicionales requerían lógica de control de estados por medio de controladores lógicos externos.
- **Solución:** Se implementó el patrón de diseño CSS-only basado en un `<input type="checkbox" id="nav-toggle">` oculto acompañado de una etiqueta `<label>` con el icono hamburguesa (`☰`). Al pulsar la etiqueta, el navegador alterna el estado `:checked` del checkbox, modificando la altura máxima (*max-height*) de la clase `.main-nav` de forma fluida mediante transiciones CSS.

### 2. Sincronización de rutas relativas en vistas secundarias
- **Problema:** Al estructurar las páginas secundarias dentro de la subcarpeta `views/`, los enlaces hacia las hojas de estilo, las imágenes y la página de inicio se rompían y cargaban sin formato visual.
- **Causa:** Las rutas relativas estándar (`css/main.css` o `img/...`) buscaban los recursos partiendo de la raíz del servidor y no desde el directorio físico donde residía el archivo HTML secundario.
- **Solución:** Se ajustaron de forma rigurosa todas las rutas de recursos en los archivos dentro de `views/` utilizando el operador de retroceso de directorio (`../`), garantizando que la ruta relativa apunte correctamente a la carpeta raíz (`../css/` y `../img/`).

### 3. Comportamiento dinámico de validación visual de formularios
- **Problema:** Los campos de texto requerían mostrar realimentación visual inmediata al usuario (bordes verdes o rojos) según lo que escribiera, pero sin interferir con el diseño base antes de la interacción.
- **Causa:** El uso de clases estáticas de validación requería validadores por evento de envío (*submit*).
- **Solución:** Se integraron las pseudo-clases nativas `:valid` y `:invalid` de HTML5/CSS3 en conjunto con los atributos de validación requeridos (`minlength`, `required`, `type="email"`). De este modo, los campos vacíos o mal formateados adoptan el color de error de manera automática, y mutan a verde de éxito únicamente cuando el contenido satisface los criterios establecidos.

### 4. Coherencia en la cuadrícula del catálogo con 20 productos
- **Problema:** Organizar una matriz de 20 productos manteniendo la responsividad fluida provocaba deformaciones en pantallas intermedias (tablets) y desalineaciones verticales en las tarjetas.
- **Causa:** El uso de floats o anchos fijos impedía la redistribución automática del espacio disponible según el ancho del dispositivo.
- **Solución:** Se implementó **CSS Grid** con la propiedad adaptable `grid-template-columns: repeat(4, 1fr)` en escritorios, reduciéndose a `repeat(2, 1fr)` en tablets mediante *media queries* (a partir de 768px) y a una sola columna `1fr` en teléfonos móviles, asegurando además que todas las tarjetas posean una estructura interna de altura flexible basada en Flexbox (`display: flex; flex-direction: column;`).

---

## 6. Estructura de Archivos del Repositorio

```text
EcoMarket/
├── index.html                  # Página principal (Home, Hero banner, Productos destacados)
├── README.md                   # Documentación técnica completa del proyecto
├── css/
│   ├── main.css                # Reset global, variables :root y tipografía
│   ├── layout.css              # Estructura general, Header, Footer y Grids Mobile First
│   ├── components.css          # Tarjetas, botones, buscador, sidebar, paginación y formularios
│   └── animations.css          # Keyframes y transiciones de microinteracción
├── img/
│   ├── products/               # Imágenes de productos (prod-1.jpg hasta prod-20.jpg)
│   ├── icons/                  # Iconos SVG vectoriales (sin-plastico, comercio-justo, redes, etc.)
│   └── hero/                   # Imágenes de banner, historia, mapa de ubicación y avatares de clientes
└── views/
    ├── productos.html          # Catálogo completo con sidebar sticky, buscador y 20 productos
    ├── sobre-nosotros.html     # Brand Story (historia en Flexbox, principios y carrusel CSS)
    └── contacto.html           # Formulario inteligente con validación CSS y mapa estilizado