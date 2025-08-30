# Radio España — MVP listo para Vercel (no técnico)

## Qué es
Una web que muestra emisoras y su **Ahora / A continuación**. Lista para subir a **Vercel** y usar **Postgres (Neon)**.

---

## Pasos súper simples

### 1) Sube este proyecto a GitHub
1. Entra en https://github.com y crea un **repositorio nuevo** (p. ej. `radio-es-mvp`).
2. Arrastra **todas** las carpetas/archivos de esta carpeta dentro del repo (usa el botón **Upload files**).
3. Pulsa **Commit**.

### 2) Crea la base de datos (Neon)
1. Ve a https://neon.tech → **Sign up** (con tu GitHub).
2. Crea un **Project** nuevo → copia la **Connection string** (empieza por `postgres://...`).

### 3) Despliega en Vercel
1. Ve a https://vercel.com → **New Project** → elige tu repo de GitHub.
2. En **Environment Variables** añade:
   - `DATABASE_URL` → pega la de Neon (`postgres://...`)
   - `ADMIN_SECRET` → inventa una clave (p. ej. `123456`)
   - `CRON_SECRET` → otra clave (p. ej. `abcxyz987`)
3. Pulsa **Deploy**. (Durante el build, se crean las tablas automáticamente).

### 4) Cargar datos (sin consola, usando Hoppscotch)
1. Abre https://hoppscotch.io
2. Método **POST** y URL: `https://TU-PROYECTO.vercel.app/api/ingest/generic-json`
3. En **Headers** añade: `Authorization` con valor `Bearer TU_ADMIN_SECRET`
4. En **Body → raw → JSON** pega el contenido de `rne_radio1.json` (te lo di en el chat) y pulsa **Send**.
5. Repite con el JSON de **Cadena 100**.
6. Abre tu web `https://TU-PROYECTO.vercel.app` y ¡listo!

> También puedes importar CSV en `POST https://TU-PROYECTO.vercel.app/api/import/schedules-csv` con el header de Authorization.

---

## ¿Dónde edito cosas?
- **Páginas**: `app/(public)`
- **API**: `app/api/...`
- **Modelos BD**: `prisma/schema.prisma`

## Notas
- El build ya ejecuta `prisma db push` automáticamente.
- Para ingestas automáticas (cada madrugada), usa `POST /api/ingest/radiodns` con `Authorization: Bearer CRON_SECRET`.

¡Suerte! 🚀
