# Catálogo de Productos con Astro y DummyJSON API

## 🎯 Propósito del sitio

Prototipo de catálogo de productos dinámico desarrollado con Astro. Muestra una grilla responsiva de productos obtenidos desde una API REST pública y permite filtrarlos en tiempo real mediante un buscador.

## 🔌 API utilizada

[DummyJSON Products](https://dummyjson.com/products)

```text
GET https://dummyjson.com/products?limit=12
```

La respuesta es un objeto con metadatos de paginación (`total`, `skip`, `limit`) y un arreglo `products`. De cada producto se usan los campos `id`, `title`, `price`, `category`, `rating` y `thumbnail`.

## 🛠️ Tecnologías

- Astro
- TypeScript / JavaScript
- CSS3 (Grid, Flexbox, variables CSS)

## 📁 Estructura

```text
src/
├── components/ProductoCard.astro
├── layouts/Layout.astro
├── pages/index.astro
└── styles/global.css
```

## 📋 Instalación y ejecución

1. Crear el proyecto (solo la primera vez):

   ```bash
   npm create astro@latest catalogo-api
   cd catalogo-api
   ```

   Si clonas un repositorio existente:

   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd catalogo-api
   ```

2. Instalar dependencias:

   ```bash
   npm install
   ```

3. Iniciar el servidor de desarrollo (disponible en `http://localhost:4321`):

   ```bash
   npm run dev
   ```

4. Generar la versión de producción y previsualizarla:

   ```bash
   npm run build
   npm run preview
   ```

## ✅ Requerimientos cumplidos

- `fetch()` a `https://dummyjson.com/products?limit=12` en el frontmatter de `index.astro`, con manejo de errores mediante `try/catch` y validación de `response.ok`.
- Componente `ProductoCard.astro` que recibe `title`, `price`, `category`, `rating` y `thumbnail` mediante `Props`.
- Lista de productos renderizada con `.map()`.
- Layout reutilizable `Layout.astro`.
- CSS Grid con `repeat(auto-fit, minmax(220px, 1fr))` y `gap: 1rem` en `global.css`.
- Diseño responsivo sin desbordamiento horizontal.
- Buscador `<input type="search" id="buscador">` con script de cliente que escucha el evento `input`, lee `data-title` y alterna el atributo `hidden`.

## 📸 Captura del sitio funcionando

La vista del catálogo quedó disponible en la ruta local:

```text
http://localhost:4321/
```

Se adjunta la captura del sitio funcionando como parte de la entrega visual del proyecto.

## 🧠 Preguntas de evaluación

### 1. ¿Qué función cumple fetch() en este proyecto?
`fetch()` realiza la petición HTTP a la API de productos para obtener datos reales en formato JSON. En este proyecto se usa para consultar `https://dummyjson.com/products?limit=12` y luego transformar la respuesta en una lista de productos renderizada en la página.

### 2. ¿Por qué utilizamos map() en lugar de escribir 12 tarjetas manualmente?
`map()` permite recorrer el arreglo de productos devuelto por la API y generar cada tarjeta de forma dinámica. Así evitamos duplicar código, el catálogo se adapta automáticamente a cualquier cantidad de productos y es más mantenible.

### 3. ¿Qué ventajas ofrece separar las tarjetas en un componente y enviarle props?
Se reutiliza la misma estructura visual para cada producto, el código queda más limpio y modular, y se reduce la repetición. Además, al enviar props como `title`, `price`, `category`, `rating` y `thumbnail`, cada tarjeta puede renderizar datos distintos sin duplicar lógica.

### 4. ¿Qué diferencia existe entre consultar la API en el frontmatter de Astro y consultarla desde JavaScript en el navegador?
En el frontmatter de Astro, la consulta se ejecuta en el servidor durante la generación de la página, lo que permite obtener datos antes de renderizar HTML. En JavaScript del navegador, la petición ocurre del lado del cliente y normalmente necesita interacción del usuario o un tiempo de carga adicional; además, la lógica de renderizado queda en el navegador.

## ⚠️ Limitaciones conocidas

- El buscador filtra solo entre los 12 productos cargados; no consulta `/products/search?q=`.
- Con la salida estática por defecto, los datos se obtienen al compilar y no se actualizan hasta volver a ejecutar `npm run build`.
