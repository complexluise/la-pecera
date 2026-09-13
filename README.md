<div align="center">

# 🐠 La Pecera

**Juego de fiesta de palabras en 3 rondas — descríbela, una sola palabra y mímica.**

Para 4 o más personas · en tu teléfono · sin instalar nada · sin internet.

</div>

---

## Cómo se juega

Se arma una "pecera" con palabras de las categorías que elijan. Se juega en
equipos y hay **tres rondas con las mismas palabras**, cada una más difícil:

1. **Descríbela** — hablás todo lo que quieras, menos la palabra.
2. **Una sola palabra** — una única pista, y a rezar.
3. **Mímica** — ni un sonido, solo el cuerpo.

Como las palabras se repiten, conviene poner atención desde la primera ronda:
lo que recuerden es lo que los salva en la tercera. Gana el equipo con más
puntos sumando las tres rondas.

Incluye cronómetro, marcador por equipos, reparto de equipos al azar o a dedo,
pase con castigo, sonido/vibración y una categoría picante (+18) opcional.

## Jugar

- **En línea:** _(URL de Firebase Hosting; se completa tras el primer deploy)_
- **Instalar como app:** abrí la URL en el teléfono y elegí "Agregar a pantalla
  de inicio". Queda como una app y funciona sin internet.

## Correr en local

Es una web app estática de un solo archivo — no hay build. El único requisito es
servirla por HTTP (el modo offline no funciona abriendo el archivo directo):

```bash
npx serve public
# o, respetando la config de hosting:
firebase emulators:start --only hosting
```

## Cómo está hecho

- **Un solo archivo:** todo el juego (HTML + CSS + JS) vive en
  `public/index.html`. Vanilla JS, sin frameworks ni dependencias en runtime.
- **PWA:** `manifest.webmanifest` + `sw.js` la hacen instalable y offline.
- **Hosting:** Firebase Hosting, con deploy automático por GitHub Actions.
- **Versionado:** [release-please](https://github.com/googleapis/release-please)
  sobre conventional commits.

Ver [`CLAUDE.md`](./CLAUDE.md) para el detalle de la estructura y el flujo de
trabajo.

## Deploy

Al mergear a `main`, GitHub Actions publica solo en Firebase Hosting (canal
`live`); los Pull Requests generan un preview con URL temporal. Ver
[`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml) y la sección de
configuración en `CLAUDE.md`.

## Licencia

[MIT](./LICENSE)
