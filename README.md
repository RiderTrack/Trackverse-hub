# 📦 TrackVerse Hub · Catálogo de Apps

Catálogo web profesional para organizar y distribuir tus APKs. Lee automáticamente los releases de tus repos de GitHub y los muestra en una página web bonita, con password, stats, QR, theme studio y panel de admin.

---

## 🎯 Características

- ✅ **Catálogo web** responsive (se ve bien en celular y PC)
- ✅ **Password protection** (público + admin separados)
- ✅ **Theme Studio** (cambiar colores desde el admin)
- ✅ **Multi-app** (RiderTrack, ClienteTrack, FitWallet, Health, etc.)
- ✅ **Versiones históricas** (ver y descargar cualquier versión anterior)
- ✅ **Stats** (descargas totales, por app, por versión)
- ✅ **QR code** por app/versión para compartir fácil
- ✅ **Buscador y filtros** por categoría
- ✅ **Auto-actualización** (no hay que subir nada manual)
- ✅ **100% gratis** (GitHub Pages + GitHub Releases)
- ✅ **Admin panel** para agregar/editar apps sin tocar código

---

## 📁 Estructura del repo

```
trackverse-hub/
├── apps.html           ← Catálogo público (con password)
├── admin.html          ← Panel de admin (con password admin)
├── apps.json           ← Base de datos (config + lista de apps)
├── release-apk.yml     ← Workflow para copiar en cada repo de app
└── README.md           ← Este archivo
```

---

## 🚀 Setup paso a paso (~30 min)

### PASO 1: Crear el repo `trackverse-hub`

1. Andá a https://github.com/new
2. Repository name: `trackverse-hub`
3. Marcar "Public" (necesario para GitHub Pages gratis)
4. ✅ Initialize with README
5. Click "Create repository"

### PASO 2: Subir los archivos

1. Subí estos 4 archivos al repo:
   - `apps.html`
   - `admin.html`
   - `apps.json`
   - `release-apk.yml` (ponelo en `.github/workflows/`)

   Podés arrastrarlos directo en la web de GitHub.

### PASO 3: Activar GitHub Pages

1. En el repo, andá a **Settings** → **Pages** (menú izquierdo)
2. Source: **Deploy from a branch**
3. Branch: `main` / `root`
4. Click **Save**
5. Esperá 1-2 min. Te da una URL tipo:
   ```
   https://rudyalen.github.io/trackverse-hub/
   ```

### PASO 4: Crear GitHub Personal Access Token

1. Andá a https://github.com/settings/tokens
2. Click **"Generate new token (classic)"**
3. Note: `TrackVerse Hub Admin`
4. Expiration: `No expiration` (o 1 año)
5. Marcá el scope: ✅ `repo` (todo el bloque)
6. Click **Generate token**
7. **Copiá el token** (empieza con `ghp_...`) — no vas a poder verlo de nuevo

### PASO 5: Configurar el admin

1. Entrá a: `https://rudyalen.github.io/trackverse-hub/admin.html`
2. Password default: `TrackVerse2026`
3. Andá al tab **⚙️ Config**
4. Pegá el token en "GitHub Personal Access Token"
5. Click **💾 Guardar token**
6. Cambiá los passwords en tab **🔐 Seguridad** (recomendado)

### PASO 6: Agregar el workflow a cada repo de app

Por cada repo (ridertrack, clientetrack, fitwallet, health, etc.):

1. Copiá el archivo `release-apk.yml`
2. En el repo de la app, creá el archivo:
   ```
   .github/workflows/release-apk.yml
   ```
3. Pegá el contenido y commit

A partir de ahora, cada `git push` a `main` va a:
- Construir el APK
- Crear un Release con el APK adjunto
- Aparecer automáticamente en el catálogo

### PASO 7: Agregar apps al catálogo

1. Entrá al admin: `https://rudyalen.github.io/trackverse-hub/admin.html`
2. Tab **📦 Apps** → **➕ Agregar app**
3. Completá:
   - Nombre: `FitWallet`
   - Icono: `💪` (emoji)
   - Color: `#f59e0b`
   - Repo: `rudyalen/fitwallet`
   - Descripción: `App de finanzas personales`
   - Categoría: `Finanzas`
4. Click **💾 Guardar**
5. ¡Listo! La app aparece en el catálogo inmediatamente

### PASO 8: Probar el flujo completo

1. Hacé un cambio chiquito en `ridertrack/index.html`
2. `git add`, `git commit`, `git push`
3. Esperá ~10 min (el workflow corre)
4. Entrá al catálogo: `https://rudyalen.github.io/trackverse-hub/`
5. Vas a ver la nueva versión de RiderTrack 🎉

---

## 🎨 Personalización

### Cambiar colores (Theme Studio)
1. Entrá al admin
2. Tab **🎨 Theme Studio**
3. Elegí los colores con los pickers
4. Click **💾 Guardar tema**

### Cambiar nombre del catálogo
1. Admin → tab **⚙️ Config**
2. Editá "Nombre del catálogo"
3. Click **💾 Guardar config**

### Cambiar passwords
1. Admin → tab **🔐 Seguridad**
2. Editá los 2 passwords
3. Click **💾 Guardar passwords**

---

## 📱 Acceso al catálogo

| URL | Para qué | Password |
|-----|----------|----------|
| `https://rudyalen.github.io/trackverse-hub/` | Ver y descargar apps | `TrackVerse2026` (default) |
| `https://rudyalen.github.io/trackverse-hub/admin.html` | Panel de admin | `TrackVerse2026` (default) |

**Cambiá los passwords cuanto antes** desde el admin.

---

## ❓ Troubleshooting

### "No veo ninguna app en el catálogo"
- Verificá que el repo de la app tenga **releases** (entrá a `github.com/rudyalen/ridertrack/releases`)
- Si no hay releases, el workflow `release-apk.yml` no está corriendo o falló
- Andá a la tab **Actions** del repo de la app para ver logs

### "El admin no guarda los cambios"
- Necesitás configurar el **GitHub Token** en tab **Config**
- Verificá que el token tenga scope `repo`
- Verificá que el token no esté expirado

### "Las stats de descargas no funcionan"
- GitHub actualiza los contadores de descarga cada ~24hs
- No es en tiempo real, hay delay

### "El catálogo se ve feo en el celular"
- Hacé refresh (tirá para abajo)
- GitHub Pages puede tardar en propagar cambios

---

## 🔐 Seguridad

- Los passwords están en texto plano en `apps.json` → no es seguridad real
- Es solo para mantener curiosos fuera
- Para seguridad real necesitás un backend (no entra en el scope de esto)
- El token de GitHub se guarda en localStorage del navegador (solo vos lo ves)
- Si compartís la PC, borrate el token después

---

## 🛠️ Stack técnico

- HTML + CSS + JavaScript puro (sin frameworks)
- GitHub Pages (hosting gratis)
- GitHub Releases API (lista las versiones)
- GitHub Contents API (editar apps.json desde el admin)
- localStorage (preferencias, token)
- 0 dependencias de Firebase, 0 pagos

---

## 📊 Límites del plan gratis de GitHub

- GitHub Pages: 100GB/mes tráfico (suficiente)
- GitHub Releases: 2GB por release (suficiente para APKs)
- GitHub Actions: 2000 min/mes (cada build tarda ~5-10 min → ~200 builds/mes)
- API calls: 5000/hora con token, 60/hora sin token

Para un catálogo personal + equipo de motoristas, no vas a llegar a ningún límite.

---

## 🚀 Roadmap (futuras mejoras)

- [ ] Notificaciones push cuando hay nueva versión
- [ ] Auto-update del APK (con service worker)
- [ ] Login con Google para stats personales
- [ ] Comentarios en cada versión
- [ ] Comparación entre versiones
- [ ] Exportar lista de descargas en CSV
- [ ] Categorías con iconos personalizados

---

## 📞 Soporte

Si algo no funciona, decime:
1. Qué URL estás intentando acceder
2. Qué esperabas ver
3. Qué ves en su lugar (screenshot ideal)
4. En qué navegador/celular

---

**TrackVerse Hub** · by Rudy Alen + Zen 🤖 · 2026
