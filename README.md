# CONCLAVE — Web + CMS

Landing page de CONCLAVE Valencia con panel de edición integrado.  
Desplegado en **Vercel** + CMS via **Decap CMS** con autenticación GitHub OAuth.

---

## Editar contenido (panel CMS)

1. Ir a `tu-dominio.com/admin`
2. Iniciar sesión con tu cuenta de GitHub
3. Editar los campos deseados
4. Pulsar **"Publicar"** — Vercel redespliegue automáticamente (~30 seg)

---

## Configuración inicial (una sola vez)

### 1. Subir el proyecto a GitHub

```bash
git init
git add .
git commit -m "Inicial: landing CONCLAVE"
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

### 2. Conectar con Vercel

- Entrar en [vercel.com](https://vercel.com) → "Add New Project"
- Importar el repositorio de GitHub
- Framework Preset: **Other**
- Build command: *(vacío)*
- Output directory: `.`
- Desplegar

### 3. Crear una GitHub OAuth App

- Ir a GitHub → **Settings** → **Developer settings** → **OAuth Apps** → "New OAuth App"
- Rellenar:
  - **Application name:** `CONCLAVE CMS`
  - **Homepage URL:** `https://tu-dominio.vercel.app`
  - **Authorization callback URL:** `https://tu-dominio.vercel.app/admin`
- Pulsar "Register application"
- Copiar el **Client ID** que aparece

### 4. Actualizar `admin/config.yml`

Abrir el archivo y sustituir los dos placeholders:

```yaml
backend:
  name: github
  repo: TU_USUARIO/TU_REPOSITORIO   # ← tu usuario y nombre de repo
  branch: main
  auth_type: implicit
  app_id: TU_GITHUB_OAUTH_APP_CLIENT_ID  # ← el Client ID copiado en el paso 3
```

Guardar, hacer commit y push. Vercel redespliegue solo.

### 5. Listo

El panel estará en `tu-dominio.vercel.app/admin`  
Los usuarios que editen contenido necesitan tener acceso al repositorio de GitHub (como Collaborator).

---

## Estructura de archivos

```
/
├── index.html          ← Web principal
├── content.json        ← Todo el contenido editable
├── vercel.json         ← Configuración de Vercel
├── admin/
│   ├── index.html      ← Panel CMS (Decap CMS)
│   └── config.yml      ← Campos editables ← EDITAR ANTES DE DESPLEGAR
└── README.md
```

---

## Contenido editable desde el panel

| Sección | Campos |
|---------|--------|
| Meta (SEO) | Título de la página, descripción |
| Hero | Tagline × 3, subtítulo, texto de apertura |
| El Concepto | Etiqueta, título, 2 párrafos, definición |
| Contacto | Título, párrafo, email, dirección, teléfono |
| Ubicación | Título, subtítulo, URL del mapa |
| Footer | Copyright |
