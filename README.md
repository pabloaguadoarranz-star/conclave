# CONCLAVE — Web + CMS

Landing page de CONCLAVE Valencia con panel de edición integrado.

---

## Editar contenido (panel CMS)

1. Ir a `tu-dominio.com/admin/`
2. Iniciar sesión con tu cuenta de Netlify Identity
3. Hacer clic en **"Contenido del sitio"**
4. Editar los campos deseados
5. Pulsar **"Publicar"** — los cambios se reflejan automáticamente en la web

---

## Despliegue en Netlify (primera vez)

### 1. Crear repositorio Git
```bash
cd CONCLAVE
git init
git add .
git commit -m "Inicial: landing CONCLAVE"
```
Sube el repositorio a GitHub/GitLab.

### 2. Conectar con Netlify
- Entrar en [netlify.com](https://netlify.com) → "Add new site" → "Import from Git"
- Seleccionar el repositorio
- Build command: *(dejar vacío)*
- Publish directory: `.`
- Desplegar

### 3. Activar Netlify Identity
- En el panel de Netlify → **Identity** → "Enable Identity"
- En **Registration** → seleccionar "Invite only"
- En **Git Gateway** → "Enable Git Gateway"

### 4. Invitar usuarios
- Identity → "Invite users" → introducir el email del cliente
- El cliente recibirá un email para crear su contraseña

### 5. Listo
El panel estará disponible en `tu-dominio.com/admin/`

---

## Estructura de archivos

```
/
├── index.html          ← Web principal
├── content.json        ← Todo el contenido editable
├── netlify.toml        ← Configuración de Netlify
├── admin/
│   ├── index.html      ← Panel CMS (Decap CMS)
│   └── config.yml      ← Campos editables
└── README.md
```

---

## Contenido editable

| Sección | Campos |
|---------|--------|
| Meta (SEO) | Título, descripción |
| Hero | Tagline × 3, subtítulo, texto de apertura |
| El Concepto | Etiqueta, título, 2 párrafos, definición |
| Contacto | Título, párrafo, email, dirección, teléfono |
| Ubicación | Título, subtítulo, URL del mapa |
| Footer | Copyright |
