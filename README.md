# Pádel · La historia de un deporte de cristal y muro

Landing page larga y de una sola página sobre la historia del pádel, desde su creación en Acapulco en 1969 hasta su expansión mundial. Toda la web está diseñada como si fuera una pista: césped azul, líneas blancas, paneles de cristal, una red y una pelota que te sigue mientras haces scroll.

Es un proyecto estático: HTML, CSS y una pequeña cantidad de JavaScript, sin dependencias ni proceso de compilación.

## Estructura del proyecto

```
.
├── index.html   # Contenido, estructura y script de la web
├── style.css    # Todos los estilos
└── README.md
```

## Cómo verlo

1. Descarga o clona el proyecto y deja `index.html` y `style.css` en la misma carpeta.
2. Abre `index.html` en tu navegador.

No necesitas instalar nada. Eso sí, las tipografías se cargan desde Google Fonts, así que hace falta conexión a internet para verlas. Sin conexión la web sigue funcionando con tipografías de respaldo (Arial Narrow o Impact para los títulos y la fuente del sistema para el texto).

Si prefieres servirlo en local:

```bash
# Con Python
python3 -m http.server 8000

# Con Node
npx serve .
```

Después abre `http://localhost:8000`.

## Secciones

| Sección | Qué contiene |
| --- | --- |
| **Hero** | La pista vista desde arriba con las líneas dibujándose al cargar y la pelota cayendo. |
| **Origen** | Acapulco, 1969, con un panel de cristal y el texto fundacional. |
| **Expansión** | Marbella, Argentina y el resto del mundo, en filas con tipografía de contorno. |
| **Cómo se juega** | Pista interactiva: cada regla ilumina su zona. |
| **Cronología** | Hitos de 1969 a hoy sobre la línea central de la pista. |
| **Leyendas** | Acordeón con jugadores y referentes del deporte. |
| **Cierre** | Llamada final con una red de malla. |

## Características de diseño

- **Estética de pista:** azul pista, azul exterior más oscuro y líneas blancas. El amarillo de la pelota se usa solo en la pelota.
- **Césped sintético:** textura generada con un SVG en línea y franjas sutiles, sin imágenes externas.
- **La "T" de la pista:** cada sección empieza con una línea de saque y su cruce con la línea central.
- **Cristal templado:** paneles con desenfoque, tornillos en las esquinas y un reflejo que se desplaza con el scroll.
- **Pelota con física simple:** sigue el scroll, rebota con sombra, se aplasta al tocar el suelo y cae cuando dejas de desplazarte.
- **Scroll suavizado:** `scroll-behavior: smooth` con margen para la navegación fija.
- **Tipografía:** [Big Shoulders Display](https://fonts.google.com/specimen/Big+Shoulders+Display) para títulos y [Hanken Grotesk](https://fonts.google.com/specimen/Hanken+Grotesk) para el texto.

## Personalización

### Colores y tipografías

Todo el tema se controla desde las variables CSS al inicio de `style.css`:

```css
:root {
  --pista: #1356a8;      /* azul de la pista */
  --exterior: #0a2f63;   /* azul oscuro de la zona exterior */
  --cristal: #eaf4ff;    /* fondo de las secciones claras */
  --resalte: #7fe0ff;    /* color de las zonas iluminadas */
  --bola: #d4ee3a;       /* color de la pelota */
  --trazo: 4px;          /* grosor de las líneas */
}
```

### Comportamiento de la pelota

Está en el bloque de script al final de `index.html`. Estos valores controlan su movimiento:

- `amp`: amplitud del recorrido de lado a lado (por defecto `0.38`, o `0.34` en pantallas pequeñas).
- `rebotes`: cuántos botes da a lo largo de la página, calculado según el alto del documento.
- `altoMax`: altura máxima de cada bote.
- `suelo`: altura del suelo respecto a la pantalla (por defecto el 80 %).

### Contenido

Los textos están directamente en `index.html`. Para añadir otro jugador al acordeón, copia un bloque `<details class="jugador" name="leyendas">` y cambia el nombre y el texto. Para añadir un hito, copia un `<li>` de la lista `.cronologia`.

## Accesibilidad

- Estructura semántica con encabezados, regiones y `aria-labelledby`.
- La pista interactiva usa `role="tablist"` y se maneja con teclado (flechas) además de con el ratón.
- Estilos de foco visibles.
- Respeta `prefers-reduced-motion`: se desactivan las animaciones de trazo, la caída de la pelota y los efectos de apertura.
- La pelota y los elementos decorativos están marcados con `aria-hidden`.

## Compatibilidad

Pensado para navegadores modernos (Chrome, Edge, Firefox y Safari actuales). Algunas notas:

- `backdrop-filter` (cristal) puede verse sin desenfoque en navegadores antiguos, pero el panel sigue siendo legible.
- El acordeón usa el atributo `name` de `<details>` para que solo se abra un jugador a la vez. En navegadores que no lo soportan, cada jugador se abre de forma independiente.
- Sin JavaScript, la web se lee con normalidad, pero la pelota no se mueve y la pista interactiva no resalta zonas.

## Notas sobre el contenido

Los datos históricos son un resumen divulgativo y algunas fechas y atribuciones, como la llegada a España o el papel de Marbella, tienen versiones distintas según las fuentes. Conviene contrastarlos antes de publicar la web. Lo mismo se aplica a las medidas de la red (88 cm en el centro y 92 cm en los extremos) y al formato de puntuación, que conviene verificar con el reglamento vigente.

## Licencia

Proyecto de uso libre. Añade aquí la licencia que prefieras (por ejemplo, MIT) si vas a publicarlo.
