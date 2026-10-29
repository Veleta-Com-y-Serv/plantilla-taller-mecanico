# Plantilla «Taller mecánico» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **industrial**
(gris carbón + naranja + blanco, franjas diagonales de señalización, titulares estrechos en mayúsculas, esquinas
achaflanadas como chapa cortada y bandas a todo el ancho de la ventana). Todo en castellano de España, frases
cortas, sin jerga. El brief de diseño completo está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`…
  - `primario` = naranja de botones, banda de marcas, banda de cifras, franjas y precios. La letra encima se calcula sola (`--sobre-primario`: negra si el primario es claro, blanca si es oscuro).
  - `acento` = naranja tostado para textos y detalles naranjas sobre fondo claro (antetítulos, iconos de servicios, notas de opiniones). Tiene que leerse sobre el fondo.
  - `texto` = color de la letra **y** de las bandas oscuras (cabecera, hero, el taller, cita, contacto; tarifas y pie usan una versión aún más oscura, `--noche`). En ellas la letra usa `fondo`. Si el cliente pide fondo oscuro, el diseño se invierte solo.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos` = Bahnschrift SemiCondensed / DIN Condensed / Roboto Condensed…, del sistema; botones `.btn` achaflanado y `.btn-sec`; bandas `.banda-clara`, `.banda-gris`, `.banda-carbon`, `.banda-noche`, `.banda-naranja`; `.rejilla-tecnica`; `.franja` de señalización; filas partidas a sangre `.partida`, `.partida--md`, `.partida-texto--izq/--der`, `.partida-foto`; cabecera, campo de matrícula, pie y barra inferior de móvil). Sin fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en chapa naranja + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas son bandas a todo el ancho.
- `hero` → `hero.astro`: foto a sangre con velo carbón y franjas en el borde derecho; `antetitulo`, `titulo` enorme, `texto`, `cta` (pedir cita) y `cta_secundario` (llamar: `url: "tel:+34…"`). Abajo, barra de utilidades con teléfono, horario y dirección de `contacto` (la dirección, desde tableta).
- `servicios` → `servicios.astro`: cabecera partida y rejilla densa con filetes (`items: [{titulo, texto, icono}]`, 6-8). Sus títulos son las opciones de «¿Qué le hacemos?» del formulario de cita. `cta` opcional.
- `marcas` → `marcas.astro`: banda naranja con los nombres de las marcas en letra enorme (`items: [{titulo}]`, solo texto, nunca logotipos). **No se pinta si `items` está vacío.**
- `sobre` → `sobre.astro` (El taller): fila partida con `imagen` a sangre a la izquierda; `texto` (párrafos separados por línea en blanco), `items: [{titulo, texto, icono}]` (compromisos), `cta`; debajo, `galeria` (lista de fotos) en franja de borde a borde.
- `cita` → `cita.astro`: mitad gris con `items` (pasos numerados) y `nota`; mitad carbón a sangre con `imagen` velada de fondo y el formulario de cita (nombre, teléfono, matrícula, marca y modelo, día, servicio, mensaje). `boton_formulario` opcional.
- `tarifas` → `tarifas.astro`: `tarifas: [{nombre, texto, precio, categoria}]` agrupadas por `categoria` en columnas, con línea de puntos y precio en naranja; `nota` al pie. Sin precio, no sale precio. **No inventes precios.**
- `cifras` → `cifras.astro`: `items: [{titulo: "+300", texto}]` en banda naranja. **No se pinta si `items` está vacío.** No inventes cifras.
- `opiniones` → `opiniones.astro`: `testimonios: [{texto, autor, nota}]` en columnas con filetes. No inventes opiniones.
- `preguntas` → `preguntas.astro`: titular fijo a la izquierda (con el teléfono) y acordeón `details/summary` a la derecha (`preguntas: [{pregunta, respuesta}]`). Sin preguntas no se pinta.
- `contacto` → `contacto.astro`: datos de `contacto` en filas grandes (teléfono enorme) y `imagen` a sangre a la derecha. Si `cita` no está activa, en lugar de la foto sale el formulario de contacto.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen` a sangre, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Procura alternar bandas claras y oscuras (`servicios`, `opiniones`, `preguntas` son claras; `marcas` y `cifras`, naranjas; el resto, oscuras).
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios y cifras siempre como texto entre comillas (`"desde 69 €"`, `"+300"`). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: servicios`, `tipo: tarifas`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y una banda a todo el ancho. `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio —tipo `AutoRepair`— y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor`, `.partida-texto`) con las fotos y fondos tocando el borde, sin scroll horizontal en móvil, botones de 48 px, barra inferior fija de móvil («Llamar» / «WhatsApp»: sale sola si hay teléfono o WhatsApp). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (del taller: `llave, freno, rueda, diagnosis, copo, engranaje, bateria, coche, aceite, grua, pintura, escudo, euro, calendario, telefono`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.
