# Checklist colaborativo · Defensa CA2

Web estática que muestra el plan de acción con **casillas marcables**. Cada vez que alguien tilda una tarea queda registrado **su nombre y la fecha/hora**, y se sincroniza en **tiempo real** entre los 3 compañeros vía Firebase. Se publica gratis con **GitHub Pages**.

Archivos:
- `index.html` — la web (todo incluido: contenido del plan + lógica).
- `README.md` — esta guía.

---

## Paso 1 — Crear el proyecto Firebase (gratis, ~5 min)

1. Entrá a https://console.firebase.google.com y logueate con una cuenta Google.
2. **Agregar proyecto** → ponele un nombre (ej. `checklist-ca2`) → podés desactivar Google Analytics → **Crear proyecto**.

## Paso 2 — Activar Realtime Database

1. En el menú izquierdo: **Compilación → Realtime Database**.
2. **Crear base de datos** → elegí la ubicación → **Iniciar en modo de prueba** → Habilitar.
3. (El modo de prueba alcanza para un trabajo de cátedra; ver nota de seguridad al final.)

Si querés dejar las reglas explícitas, en la pestaña **Reglas** pegá esto y publicá:

```json
{
  "rules": {
    "tasks": {
      ".read": true,
      ".write": true
    }
  }
}
```

## Paso 3 — Obtener la configuración web

1. Ícono de engranaje → **Configuración del proyecto**.
2. En **Tus apps**, tocá el ícono web **`</>`**, registrá la app (cualquier apodo, sin hosting).
3. Firebase te muestra un objeto `firebaseConfig`. Copialo.

## Paso 4 — Pegar la config en `index.html`

1. Abrí `index.html` con cualquier editor de texto.
2. Buscá el bloque `const firebaseConfig = { ... }` (cerca del final).
3. Reemplazá los `"PEGA_AQUI"` por tus valores reales. Tiene que quedar el `databaseURL` (algo como `https://checklist-ca2-default-rtdb.firebaseio.com`).
4. Guardá.

> Mientras quede algún `PEGA_AQUI` en `databaseURL`, la web funciona igual pero en **modo local** (cada uno ve solo sus marcas). Con la config real → se comparte en vivo.

## Paso 5 — Publicar en GitHub Pages

1. Creá un repositorio nuevo en https://github.com (público).
2. Subí `index.html` (y `README.md`) — botón **Add file → Upload files → Commit**.
3. En el repo: **Settings → Pages**.
4. En **Build and deployment → Source** elegí **Deploy from a branch**, rama `main`, carpeta `/ (root)` → **Save**.
5. Esperá ~1 min. Te queda una URL tipo `https://TU-USUARIO.github.io/TU-REPO/`.
6. Pasale ese link a tus compañeros.

---

## Cómo se usa

1. Cada uno abre el link y escribe **su nombre** arriba (queda guardado en su navegador).
2. Al **tildar** una casilla se guarda con su nombre + fecha; al **destildar** se borra.
3. La barra de progreso y los contadores por sección (ej. `12/50`) se actualizan solos.
4. Todos ven los cambios de todos en tiempo real.

## Actualizar el contenido del plan

El texto del plan está embebido dentro de `index.html`, en el bloque
`<script type="text/plain" id="plan"> ... </script>`.
Si cambiás el plan en Obsidian y querés reflejarlo, reemplazá ese texto por el nuevo Markdown y volvé a subir el archivo.

> Nota: los IDs de las casillas se derivan del texto de cada tarea. Si reescribís mucho una tarea, esa casilla se reinicia (se considera nueva).

## Nota de seguridad

El modo de prueba / reglas abiertas deja la base **leíble y escribible por cualquiera que tenga el link**. Para un checklist de cátedra está bien. Si querés cerrarlo, se puede agregar autenticación de Firebase más adelante.
