# Cockpit AGI Eléctrica

Panel único (Panel Financiero + Cuentas por Cobrar + Horas Hombre) para AGI SPA / Empresa Eléctrica. Cualquiera con acceso sube su Excel del mes, el navegador lo procesa, y el resumen queda guardado para que **todos los que abran el link vean lo mismo, al instante** (se actualiza solo, sin recargar).

Es un sitio estático de un solo archivo (`index.html`, sin build, sin `npm install`) más una base de datos real en Supabase que ya está creada y funcionando. Solo falta publicarlo en algún lado.

## Ya está hecho

- Tablas `agi_snapshots` y `agi_allowed_users` creadas en el proyecto Supabase **"Contabilidad - Finanzas"** de la organización Trei Inmobiliaria (esquema `public`, con prefijo `agi_` para no mezclarse con las tablas contables — no se tocó ninguna tabla existente).
- Seguridad a nivel de fila (RLS): nadie ve ni escribe nada sin haber iniciado sesión con un correo de la lista blanca. Verificado con una llamada anónima real a la API — devuelve `[]`, no expone datos.
- Lista blanca inicial (tabla `agi_allowed_users`): `smendez@trei.cl`, `abalboa@trei.cl`, `jmontecinos@trei.cl`. **Revisa que tu correo esté correcto** — si me equivoqué o falta alguien, dime el correo exacto y lo corrijo con una consulta SQL (toma un minuto).
- El flujo completo (login con código por correo → carga de datos → visualización) se probó de punta a punta con datos simulados; sin errores.

## Cómo entra la gente (sin contraseña)

1. Escriben su correo `@trei.cl`.
2. Supabase les manda un código de 6 dígitos por correo (esto ya está activo, no hay nada que configurar).
3. Si el correo está en la lista blanca, entran. Si no, ven un mensaje pidiendo que te contacten.

No hay contraseñas que administrar ni cuentas que crear a mano.

## Publicarlo (elige una)

### Opción A — Netlify, arrastrar y soltar (más rápido, sin GitHub)

1. Entra a **[app.netlify.com/drop](https://app.netlify.com/drop)** con cualquier cuenta (puedes crear una gratis con tu correo).
2. Arrastra la carpeta `agi-electrica-panel` completa (o solo `index.html`) a la página.
3. Netlify te da un link al instante (algo como `https://nombre-al-azar.netlify.app`). Ese es el link que le pasas a Alex y José Miguel.
4. Opcional: en "Site settings" puedes ponerle un nombre más lindo al subdominio.

Para actualizar el sitio más adelante (si le pido cambios), vuelves a arrastrar la carpeta actualizada al mismo sitio.

### Opción B — GitHub Pages

1. Crea un repositorio nuevo en GitHub (puede ser privado).
2. Sube estos dos archivos (`index.html`, `README.md`) — desde la web de GitHub sirve "Add file → Upload files", no hace falta usar la terminal.
3. En el repo: **Settings → Pages → Source: "Deploy from a branch" → branch `main` / carpeta `/ (root)`**.
4. En un par de minutos GitHub te da el link (`https://tu-usuario.github.io/tu-repo/`).

No encontré un conector de GitHub disponible para conectarlo a esta sesión y subir el código yo directamente — reviso el registro de Claude y no aparece uno instalable ahora mismo, así que te dejo el archivo listo para que lo subas tú (5-10 minutos siguiendo cualquiera de las dos opciones de arriba).

## Qué pasa con los datos

- El Excel se lee siempre en el navegador de quien lo sube (nunca se sube el archivo original a ningún lado).
- Lo que sí se guarda es el **resumen ya calculado** (los mismos números que ves en pantalla: totales de ingresos/egresos, presupuesto por proyecto, saldos por cliente, horas por persona) — eso es lo que permite que el panel se actualice para todos.
- Cada carga queda con el nombre y correo de quien la subió, visible en el panel (por transparencia y trazabilidad).

## Si quieres agregar o quitar a alguien

Dime el correo y si es para agregar o quitar, y lo actualizo directamente en la tabla `agi_allowed_users` — no requiere tocar el código ni volver a publicar el sitio.

## Nota aparte (no relacionada con este panel)

Al revisar el proyecto Supabase "Contabilidad - Finanzas" para instalar esto, el asesor de seguridad de Supabase marcó varias vistas existentes (`g_balance_q`, `g_estado_resultados_q`, entre otras) como `SECURITY DEFINER`, lo que puede saltarse los permisos normales de fila. Es un hallazgo preexistente, no algo que haya tocado yo — lo dejo anotado para quien administre ese proyecto, por si vale la pena revisarlo.
