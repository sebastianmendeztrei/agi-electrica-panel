# Cockpit AGI Eléctrica

Panel único (Panel Financiero + Cuentas por Cobrar + Horas Hombre) para AGI SPA / Empresa Eléctrica. Está publicado en **https://sebastianmendeztrei.github.io/agi-electrica-panel/**.

Es un sitio estático de un solo archivo (`index.html`, sin build, sin `npm install`) y sin backend: no hay login, no hay base de datos, no hay nada que se comparta entre quienes lo abren. Cada Excel que se suelta ahí se procesa **solo en el navegador de quien lo sube** — nunca se envía a ningún servidor, y no queda guardado para que otros lo vean.

## Cómo funciona el flujo de trabajo

1. Alex (o José Miguel) te mandan el Excel del mes a ti, como ya hacían antes — por correo o WhatsApp.
2. Abres el link del panel y sueltas ahí el Excel que te mandaron, para verlo actualizado en tu propio navegador.
3. Si quieres que la versión pública (el link que le compartes a otros) muestre esos números, me pasas el mismo Excel a mí en el chat y yo actualizo el `index.html` publicado con esos datos.

Esto es a propósito más simple que una versión con login y base de datos compartida: nadie más que tú puede escribir datos en el panel, y no depende de ningún servicio de pago ni de una base de datos de terceros.

## Qué pasa con los datos

- El Excel se lee siempre en tu navegador; el archivo nunca sale de tu equipo.
- Lo que ves en pantalla (totales de ingresos/egresos, presupuesto por proyecto, saldos por cliente, horas por persona) es un cálculo que se hace ahí mismo, en memoria — se pierde si cierras o recargas la pestaña.
- Si quieres que otra persona vea esos mismos números sin que ella suba el Excel, la única forma es que tú (o yo, con tu Excel) actualicen la versión publicada.

## Publicarlo de nuevo si algo cambia

El sitio ya está en GitHub Pages, sirviendo directo desde el repo `sebastianmendeztrei/agi-electrica-panel` (rama `main`, carpeta raíz). Para actualizarlo:

1. Pídeme que actualice `index.html` (por ejemplo, con datos nuevos o un cambio de diseño).
2. Yo subo el archivo actualizado al repo — el sitio se refresca solo en un par de minutos, sin que tengas que hacer nada más.

Si en algún momento prefieres subirlo tú mismo: en GitHub, entra al archivo `index.html` del repo, usa el lápiz (editar), pega el contenido nuevo y confirma el cambio ("Commit changes").
