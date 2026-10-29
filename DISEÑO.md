# Taller mecánico: brief de diseño

Plantilla `taller-mecanico` creada el 29/10/2026 a partir de `reformas-oficios` con `php artisan plantillas:nueva`
y rediseñada entera (fila 10 del brief de la tanda «a ancho completo»). Este fichero se queda en el repo: es lo
que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: talleres mecánicos multimarca, de neumáticos, de chapa y pintura, centros de pre-ITV y
  concesionarios pequeños (`sectores`: taller, mecanico, neumaticos, chapa-pintura, itv, concesionario). Su
  cliente entra con el coche averiado o con la revisión pendiente: quiere el teléfono, saber si le atienden
  hoy, cuánto le va a costar más o menos y si se fía.
- **Qué tiene que conseguir la web**: que llamen o pidan cita. Teléfono en la cabecera, en la barra del hero, en
  preguntas, en contacto, en el pie y en la barra fija de móvil; «Pedir cita» en cabecera, hero y servicios.
- **Tono y estilo** (`estilo: industrial`): serio, directo y de oficio. Referencia que sí: losmartesnohayluna.com
  por las bandas a sangre y la tipografía grande; la señalética de un taller (franjas de seguridad, chapa,
  cuadro de mandos). Que no: la caja centrada estrecha con tarjetas blancas; el amarillo obra con Arial Black y
  bordes en diagonal de `reformas-oficios` (de la que parte, pero no se le debe parecer).
- **Paleta de ejemplo**: primario `#ff6b1a` (naranja), acento `#b8430b` (naranja tostado, legible sobre blanco),
  fondo `#ffffff`, texto `#1f2226` (gris carbón). Derivados en `global.css` con `color-mix`: `--noche` (carbón +
  negro: tarifas y pie), `--superficie` (gris muy claro: cita y preguntas), `--linea`. `--sobre-primario` decide
  letra negra o blanca sobre el naranja (oklch). La placa de la matrícula usa sus colores fijos (blanco y azul).
- **Tipografía**: del sistema. Títulos estrechos en mayúsculas (`Bahnschrift SemiCondensed`, `DIN Condensed`,
  `Roboto Condensed`, `Arial Narrow`; `font-stretch: condensed`, 700), interlineado 0,9; el título del hero llega
  a 7,5 rem en escritorio (2,9 en móvil). Cifras y precios con la misma familia y números tabulares (`.num`).
  Antetítulos en mayúsculas espaciadas (0,2 em) con una franja de señalización delante. Texto en `system-ui`.
- **Formas**: botones y chapas (inicial del logo, iconos, números de los pasos, «+» de las preguntas) con la
  esquina inferior derecha cortada (`clip-path`); franjas diagonales naranja/carbón como separadores; rejilla
  técnica tenue sobre las bandas más oscuras.
- **Ritmo de bandas** (todas de borde a borde; contenido hasta 90 rem, 16 px de margen en móvil):
  1. `hero` — foto a sangre con velo carbón, 88 svh (pantalla completa menos cabecera en móvil y tableta),
     franjas en el borde derecho; abajo, barra de utilidades (teléfono enorme, horario, dirección).
  2. `servicios` — blanco; cabecera partida; rejilla de 4×2 (2 en tableta, 1 en móvil) con filetes y números.
  3. `marcas` — naranja entre dos franjas carbón; nombres de marcas en letra enorme separados por barras.
  4. `sobre` — carbón; 50/50 con la foto a sangre a la izquierda (desde 768 px) y franja en la esquina; debajo,
     cuatro fotos de borde a borde sin márgenes.
  5. `cita` — partida: gris claro con pasos numerados y nota en sello naranja; carbón a sangre con foto velada y
     el formulario (desde 1024 px lado a lado).
  6. `tarifas` — carbón oscuro con rejilla técnica; tres columnas por categoría con línea de puntos y precio.
  7. `cifras` — naranja; cuatro números enormes separados por filetes, como un cuadro de mandos.
  8. `opiniones` — blanco; tres columnas con filetes y comillas naranjas.
  9. `preguntas` — gris claro; titular fijo a la izquierda con el teléfono, acordeón a la derecha.
  10. `contacto` — carbón 50/50: datos grandes a la izquierda, fachada del taller a sangre a la derecha.
  Pie: carbón oscuro con franja arriba y cuatro columnas. Barra fija de móvil: «Llamar» naranja y «WhatsApp».
- **Apartados y listas propias**: `marcas.items` (`titulo`), `sobre.galeria` (rutas), `cita.items` (pasos),
  `tarifas.tarifas` (`nombre, texto, precio, categoria`). Las que salen vacías no se pintan (marcas, cifras) o
  pintan solo su titular (tarifas, opiniones).
- **Fotos** (`fotos.json`, 8): interior del taller con un coche en el elevador (hero), panel de herramientas (el
  taller), diagnosis, equilibradora, disco y pinza de freno, vano motor (galería), mostrador de recepción (cita) y
  fachada de la nave (contacto). Sin texto legible, sin logotipos, sin matrículas legibles ni personas.
- **Qué no hacer**: tarjetas blancas flotando en una caja estrecha; bordes de sección en diagonal y amarillo
  obra (son de `reformas-oficios`); logotipos de marcas de coches; precios o cifras inventados en los
  componentes.
