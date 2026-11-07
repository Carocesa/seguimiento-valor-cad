# Seguimiento de valor CAD

Sitio estático publicado con GitHub Pages. La primera pantalla es la de acceso de la demo de diseño de REP-43
(exportada con `export-demo` el 2026-11-07): pide el correo del visitante, lo registra con la fecha y hora de ingreso
(hora de Colombia) en Formspree y pasa al tablero general.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Pantalla de acceso (la `pages/access.html` de la demo, adaptada). Un correo válido registra el ingreso y abre el tablero. |
| `pages/general-dashboard.html` | El tablero general, tal cual salió de la demo. |
| `assets/` | CSS e imágenes de la demo, tal cual. |
| `.nojekyll` | Le dice a GitHub Pages que publique los archivos tal cual, sin procesarlos. |

## Qué cambió respecto a la demo exportada

- `index.html` nace de `pages/access.html`: las rutas `../assets/` pasan a `assets/`, el enlace al tablero a `pages/general-dashboard.html`.
- El formulario ya no simula el "link mágico": valida el correo, lo registra en Formspree y navega al tablero.
  Por eso el subtítulo dice "Ingresa tu correo para consultar el tablero…" y el botón "Ingresar" (antes "Enviarme el link").
- Se quitó el panel flotante "Estados" de la pantalla de acceso (era para revisar la maqueta). El del tablero sigue ahí.
- Los ajustes están al inicio del `<script>` final de `index.html`:
  - `FORMSPREE_ENDPOINT`: dónde se registran los ingresos.
  - `DASHBOARD_URL`: a qué página pasa tras el correo.
  - `ALLOWED_DOMAIN`: vacío acepta cualquier correo válido; `'cesa.edu.co'` acepta solo ese dominio.

## Configurar el registro de ingresos (Formspree)

1. Crea una cuenta gratis en <https://formspree.io> y pulsa **New form**. Nombre sugerido: `Ingresos tablero CAD`.
2. En la pestaña **Integration** copia el endpoint. Tiene la forma `https://formspree.io/f/abcdwxyz`.
3. Abre `index.html` y reemplaza `https://formspree.io/f/TU_ID_DE_FORMSPREE` por tu endpoint.
4. Sube el cambio. El **primer registro** que llegue te pedirá confirmar tu correo en Formspree; hasta que confirmes, no se guarda nada.
5. Los registros se ven en **Formspree → tu form → Submissions**, con las columnas `email`, `fecha` y `hora`, y también llegan a tu correo.

Límite del plan gratuito: 50 registros al mes. Si se supera, el tablero se sigue mostrando pero los ingresos extra no se guardan.

Mientras el endpoint sea el de ejemplo, la pantalla deja pasar sin registrar (solo avisa en la consola del navegador).

## Publicar por primera vez

1. Crea el repo en GitHub: <https://github.com/new>, nombre `seguimiento-valor-cad`, **Public**, sin README.
2. Sube el código. Sin terminal: en el repo vacío pulsa **uploading an existing file**, arrastra `index.html`, `README.md`,
   `.nojekyll` y las carpetas `pages` y `assets` completas, y pulsa **Commit changes**. Con terminal:

   ```bash
   git remote add origin https://github.com/TU-USUARIO/seguimiento-valor-cad.git
   git push -u origin main
   ```

3. En el repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.
4. En uno o dos minutos la página queda en `https://TU-USUARIO.github.io/seguimiento-valor-cad/`.

## Publicar cambios

Sin terminal: **Add file → Upload files**, arrastra los archivos cambiados (se sobrescriben) y **Commit changes**. Con terminal:

```bash
git add -A
git commit -m "Describe el cambio"
git push
```

GitHub Pages se actualiza solo en uno o dos minutos.

## Actualizar el tablero desde una nueva exportación

1. Exporta de nuevo la demo con `export-demo`.
2. Copia `pages/general-dashboard.html` y la carpeta `assets/` de la exportación sobre las de aquí.
3. No copies `pages/access.html` ni el `index.html` de la demo: el `index.html` de este repo ya es la pantalla de acceso adaptada.
   Si la pantalla de acceso cambió en el diseño, hay que volver a aplicar sobre ella los cambios de la sección anterior.
4. Sube los cambios.

## Limitaciones

- La pantalla de correo es un bloqueo visual, no seguridad: cualquier persona puede abrir `pages/general-dashboard.html` directo si conoce la URL. El tablero es público.
- Si Formspree falla o no responde, el visitante igual pasa al tablero.
