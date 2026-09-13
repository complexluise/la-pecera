# La Pecera

Juego de fiesta de palabras en 3 rondas (tipo *fishbowl*/charadas), en español.
Se juega en el teléfono, para 4 o más personas repartidas en equipos. Las tres
rondas usan **las mismas palabras**: (1) descríbela hablando, (2) una sola
palabra de pista, (3) mímica.

## Qué es esto, técnicamente

Una **web app estática de un solo archivo**: todo el juego —marcado, estilos y
lógica— vive en `public/index.html`, sin build ni dependencias en runtime. Es
además una **PWA instalable y offline** (manifest + service worker).

No hay backend, ni base de datos, ni framework. Vanilla JS. El estado de una
partida vive en memoria (objeto `S`) y no se persiste entre recargas.

## Estructura

```
public/                     # raíz que sirve Firebase Hosting
  index.html                # TODO el juego (HTML + CSS + JS inline)
  manifest.webmanifest      # metadata PWA
  sw.js                     # service worker (app shell offline)
  favicon.svg               # ícono vectorial (fuente de los PNG)
  icons/                    # PNG 192/512 normales y maskable
firebase.json               # config de Hosting (headers, cleanUrls)
.firebaserc                 # proyecto Firebase de destino (fuente única)
release-please-config.json  # versionado automático (tipo "simple")
.github/workflows/          # release-please + deploy a Firebase
```

## Trabajar con el código

Todo pasa en `public/index.html`. Bloques principales dentro del `<script>`:

- `CATS` — banco de palabras por categoría (incluye una categoría `spicy` +18).
- `ROUNDS` / `RULES` — textos de las 3 rondas y las reglas generales.
- `S` — objeto de estado global de la partida.
- Flujo de pantallas: `screen(id)` alterna `<section class="screen">` por id.
  Orden: home → setup → teams → round → ready → play → turn → rend → end.
- Juego: `startTurn` / `tickFn` (cronómetro) / `nextWord` / `hit` / `pass` /
  `endTurn` / `endRound` / `endGame`.

Convenciones: `$`/`$$` son atajos de `querySelector(All)`; toda interpolación de
texto de usuario pasa por `esc()` para evitar inyección de HTML.

### Correr en local

No hay build. Servir la carpeta `public/` por HTTP (el service worker no
funciona con `file://`):

```bash
firebase emulators:start --only hosting   # opción A, respeta firebase.json
# o
npx serve public                          # opción B, servidor estático simple
```

### Si tocás assets del service worker

Subí `CACHE_VERSION` en `public/sw.js` cuando cambien los archivos precacheados
(index, manifest, íconos), si no los clientes viejos siguen sirviendo la versión
cacheada.

### Si cambiás el ícono

Editá `public/favicon.svg` y regenerá los PNG con `sharp`:

```bash
# density alto para bordes nítidos; genera 192/512 normal y maskable
node -e "const s=require('sharp'),fs=require('fs');const svg=fs.readFileSync('public/favicon.svg');[['icon-192',192],['icon-512',512],['icon-maskable-192',192],['icon-maskable-512',512]].forEach(([n,z])=>s(svg,{density:384}).resize(z,z).png().toFile('public/icons/'+n+'.png'));"
```

## Deploy

Producción se publica sola: al mergear a `main`, el workflow `deploy.yml`
publica el canal `live` de Firebase Hosting. Los PR generan un canal de preview
con URL temporal. Requiere el secret `FIREBASE_SERVICE_ACCOUNT`.

Deploy manual (si hace falta): `firebase deploy --only hosting`.

## Disciplina git (Kybernetikcs / GitFlow-lite)

- Ramas: **`main`** = producción (siempre desplegable), **`dev`** = integración.
  El trabajo sale de `dev`; los releases van `dev → main`.
- **Conventional commits** obligatorios (`feat:`, `fix:`, `docs:`, `chore:`…):
  son lo que alimenta a release-please para versionar y armar el CHANGELOG.
- Versionado y CHANGELOG los maneja **release-please** — no editar versiones a
  mano. Pre-1.0: `feat` → minor, `fix` → patch.
- Hotfix de un bug urgente: rama desde `main`, PR a `main`, y back-merge a `dev`.

Comandos del flujo disponibles como skills: `/flujo`, `/abrir-issue`,
`/feature-cycle`, `/release`, `/hotfix`, `/graduar-adr`, `/cosechar-sesion`.
