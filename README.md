# Plantilla NoExpertise · Taller mecánico

Web industrial a todo el ancho para talleres: servicios, marcas, tarifas claras y cita previa con matrícula.

- Sectores: taller, mecánica, neumáticos, chapa y pintura, ITV y pre-ITV, concesionario. Estilo: industrial. Plan mínimo: gratis.
- Secciones: hero, servicios, marcas, sobre (el taller), cita, tarifas, cifras, opiniones, preguntas, contacto (+ `texto` para apartados nuevos).
- Campos propios: `marcas.items` (solo nombres; no se pinta vacía), `sobre.galeria` (franja de fotos), `cita.items` (pasos), `cita.nota`, `cita.boton_formulario`, `tarifas.tarifas[]` (`nombre, texto, precio, categoria`; agrupadas por categoría), `tarifas.nota`, `cifras.items` (no se pinta vacía).
- Formulario de cita previa con matrícula (aspecto de placa), marca y modelo, día preferido y servicio (las opciones salen de `servicios.items`); sin servidor (`mailto`).
- Barra inferior fija en móvil con «Llamar» y «WhatsApp».
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`AutoRepair`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.
