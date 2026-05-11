# Glance Dashboard — Extensión Firefox

Un dashboard minimalista para la nueva pestaña de Firefox, inspirado en [Glance](https://github.com/glanceapp/Glance), con tipografía estilo Apple (DM Sans + DM Serif Display + DM Mono).

---

## Archivos incluidos

```
firefox-dashboard/
├── manifest.json      ← configuración de la extensión
├── dashboard.html     ← el dashboard completo (HTML + CSS + JS)
├── icon.svg           ← icono de la extensión
└── README.md
```

---

## Instalación en Firefox (modo desarrollador)

### Paso 1 — Preparar los archivos
Descarga o copia los tres archivos en una carpeta local, p. ej. `~/glance-dashboard/`.

### Paso 2 — Abrir el gestor de extensiones temporal
1. Abre Firefox y ve a `about:debugging` en la barra de direcciones.
2. Haz clic en **"Este Firefox"** (panel izquierdo).
3. Pulsa **"Cargar complemento temporal..."**.
4. Selecciona el archivo `manifest.json` dentro de tu carpeta.

✅ La extensión se activa. Abre una nueva pestaña (`Ctrl+T`) para ver el dashboard.

> **Nota:** Las extensiones temporales desaparecen al cerrar Firefox.  
> Para tenerla siempre, sigue el paso de firma más abajo.

---

## Instalación permanente (sin firma oficial)

1. Ve a `about:config` en Firefox.
2. Busca `xpinstall.signatures.required` y ponlo en **false**.
3. Comprime la carpeta como `.zip`, renómbrala a `.xpi`.
4. Arrastra el `.xpi` sobre Firefox → confirma la instalación.

---

## Características

| Widget | Descripción |
|---|---|
| **Reloj** | Hora en tiempo real con fecha |
| **Búsqueda** | Escribe una URL o búsqueda Google y pulsa Enter |
| **Hacker News** | Top stories via API de Algolia (actualizable) |
| **Bookmarks** | Tus marcadores de Firefox (requiere permiso `bookmarks`) |
| **Notas rápidas** | Persisten entre sesiones con `localStorage` |
| **Mercados** | Datos de ejemplo (ver sección de personalización) |
| **Clima** | Placeholder estático (ver sección de personalización) |

---

## Personalización

Edita `dashboard.html` directamente:

### Cambiar ciudad del clima
Integra la API gratuita de [Open-Meteo](https://open-meteo.com/) (sin API key):
```js
const res = await fetch('https://api.open-meteo.com/v1/forecast?latitude=40.41&longitude=-3.70&current_weather=true');
```

### Actualizar cotizaciones reales
Usa la API gratuita de [Frankfurter](https://www.frankfurter.app/) para divisas o
[Yahoo Finance unofficial](https://query1.finance.yahoo.com/v8/finance/chart/AAPL) para acciones.

### Cambiar fuentes
Sustituye los `@import` de Google Fonts por cualquier otra combinación.
Las variables CSS están en `:root` al inicio del `<style>`.

### Añadir más feeds RSS
Usa un proxy CORS como `https://api.rss2json.com/v1/api.json?rss_url=TU_RSS_URL` para cargar cualquier feed.

---

## Colores y tema

Edita las variables CSS en `:root`:
```css
--bg: #0d0d0d;         /* fondo principal */
--accent-warm: #c8b89a; /* color dorado de acento */
--green: #5a9a6a;       /* positivo en markets */
--red: #d16666;         /* negativo en markets */
```

Para cambiar a tema claro, invierte los valores de `--bg` y `--text-primary`.
