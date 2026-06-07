# CONCLAVE — Progreso de sesión

## Estado actual
El proyecto está **desplegado y funcionando** en https://conclave-blush.vercel.app  
Repositorio GitHub: `pabloaguadoarranz-star/conclave`  
**Pendiente:** Activar el acceso al panel CMS (`/admin`)

---

## Lo que se ha construido

### 1. Landing page (`index.html`)
Una single-page con las siguientes secciones:
- **Hero** — Pantalla completa con efecto de humo animado (Canvas, partículas), logotipo CONCLAVE con cruz patriarcal integrada en la "C", tagline "Comer · Beber · Pecar"
- **El Concepto** — Texto de marca con definición etimológica y símbolo decorativo
- **Contacto** — Formulario (lista de espera, eventos, grupos) + datos de contacto (email, dirección, teléfono)
- **Ubicación** — Mapa de Google Maps embed + dirección
- **Footer** — Logo, tagline, navegación, copyright

Todo el texto se inyecta dinámicamente desde `content.json` via `fetch` al cargar la página.

### 2. Identidad visual aplicada
Basada en los documentos de branding del cliente (PDFs aportados):
- **Paleta de colores:**
  - `#470D25` Cremisi del Cardinale (carmesí oscuro)
  - `#5A4C35` Aurum Cónclave (dorado tierra)
  - `#272424` Fumus Sacri (negro humo) — fondo principal
  - `#1B1F32` Nox / Notte Vaticana (azul noche)
  - `#DFD2BD` Calx Vatica (pergamino crema) — texto principal
- **Tipografías:** Cinzel (headings), Cormorant Garamond (body), Raleway (UI/labels)
- **Efecto hero:** Fumata negra animada con Canvas (simulación de partículas de humo denso, con toque cármesi)

### 3. Sistema de contenido (`content.json`)
Archivo JSON con todos los textos editables. El HTML lee este archivo al cargar y popula la página. Los elementos editables llevan atributos `data-content="seccion.campo"` o `data-content-nl` (para saltos de línea).

**Estructura del JSON:**
```
meta        → titulo, descripcion (SEO)
hero        → tagline_1/2/3, subtitulo, proximamente
concepto    → label, titulo, parrafo_1, parrafo_2, definicion
contacto    → label, titulo, parrafo, email, direccion, telefono
ubicacion   → titulo, subtitulo, mapa_url
footer      → copyright
```

### 4. CMS (`admin/`)
- **Motor:** Decap CMS v3 (antiguo Netlify CMS), cargado desde CDN
- **Backend:** GitHub (autenticación OAuth con `auth_type: implicit`)
- **Panel:** `https://conclave-blush.vercel.app/admin`
- **Flujo:** El usuario edita en el panel → Decap CMS hace commit a GitHub → Vercel redespliegue automático (~30 seg)

---

## Pendiente para activar el CMS

El único paso que falta es completar la configuración de GitHub OAuth:

### Paso 1 — Crear la GitHub OAuth App (el cliente/agencia lo hace en GitHub)
- Ir a: `github.com → Settings → Developer settings → OAuth Apps → New OAuth App`
- Rellenar:
  - **Application name:** `CONCLAVE CMS`
  - **Homepage URL:** `https://conclave-blush.vercel.app`
  - **Authorization callback URL:** `https://conclave-blush.vercel.app/admin`
- Pulsar "Register application" y copiar el **Client ID**

### Paso 2 — Actualizar `admin/config.yml`
Sustituir el placeholder en la línea 6:
```yaml
app_id: TU_GITHUB_OAUTH_APP_CLIENT_ID  # ← pegar el Client ID aquí
```

### Paso 3 — Commit y push
```bash
git add admin/config.yml
git commit -m "CMS: configura GitHub OAuth App ID"
git push
```
Vercel redespliegue automáticamente. El panel en `/admin` funcionará al instante.

---

## Estructura de archivos

```
/
├── index.html          ← Web principal (lee content.json al cargar)
├── content.json        ← Todo el contenido editable
├── vercel.json         ← Configuración de Vercel (headers, cleanUrls)
├── admin/
│   ├── index.html      ← Panel CMS (Decap CMS desde CDN)
│   └── config.yml      ← Campos editables + backend GitHub ← EDITAR (app_id)
├── .gitignore
├── README.md           ← Instrucciones completas de despliegue
└── progress.md         ← Este archivo
```

---

## Notas técnicas

- La sección "El Espacio" (renders del local) fue eliminada a petición del cliente — no tenían imágenes definitivas
- El efecto de humo usa Canvas con un pool de hasta 500 partículas, spawn de 3 partículas cada 2 frames, con trail `rgba(8,6,6,0.12)` para densidad
- El mapa de Google Maps lleva `filter: grayscale(1) invert(1)` para adaptarse al tema oscuro
- El proyecto NO usa ningún framework ni bundler — HTML/CSS/JS puro, cero dependencias de node
