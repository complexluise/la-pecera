# 0001. Posicionar La Pecera como experimento de marca / lead-gen de Sostaina

- **Estado:** Aceptado
- **Fecha:** 2026-09-13
- **Origen:** charla con el PO. No hubo RFC ni discusión escrita previa; esta es
  la primera vez que la decisión queda registrada.

## Contexto

La Pecera es hoy una **PWA estática** (`public/index.html`, sin build, sin
dependencias en runtime), instalable y offline, publicada en Firebase Hosting
(`lapecera-juego.web.app`), versión v0.1.0. **No hay analítica, ni cuentas de
usuario, ni backend.** El estado de una partida vive solo en memoria y no se
persiste.

La infraestructura de Firebase ya está montada, así que Firestore, Auth y
Functions están **a un paso** de habilitarse si hicieran falta. Eso abre la
pregunta de fondo: ¿qué es La Pecera para el negocio y cómo se justifica seguir
invirtiendo en ella?

Se evaluaron cuatro caminos de monetización/rol de negocio:

- **B2B para eventos** (vender el juego o experiencias a empresas/agencias).
- **B2C freemium** (features o mazos pagos sobre el juego gratis).
- **Marca / lead-gen** (el juego como top-of-funnel de Sostaina).
- **Patrocinio** (marcas que pagan por aparecer).

El PO eligió **marca / lead-gen** como la apuesta primaria a validar. La premisa
que ordena todo lo demás: **un experimento se gana con aprendizaje barato, no
con features.**

## Decisión

**Posicionamos La Pecera como un experimento de MARCA / LEAD-GEN de Sostaina.**
El juego es _top-of-funnel_ del negocio real de la empresa, **no** un producto
que cobra directo (todavía). Su trabajo es capturar atención y contactos para
Sostaina, y el roadmap se ata a **aprendizaje**, no a features.

Trabajamos por **fases, de barato a caro**, deteniéndonos en cuanto los datos no
justifiquen la siguiente:

0. **Instrumentar** con analítica _privacy-first_ + consentimiento, y un loop de
   **compartir el resultado** de la partida.
1. **Generador de mazos con IA (Claude)** como gancho de contenido.
2. **Validar demanda** con "puerta falsa" / concierge **antes** de construir
   pagos o cuentas.

(Las fases marcan el orden de la apuesta, no un plan detallado; cada una se
decide con datos de la anterior.)

**No-goals ahora** (explícitos, no se construyen hasta que los datos lo
justifiquen):

- Cuentas de usuario.
- Pagos / cobro.
- Freemium B2C.

**Métricas de éxito** — orientadas a atención y contactos captados para
Sostaina, **no** a ingresos directos: visitas, partidas iniciadas y
completadas, instalaciones de la PWA, compartidos, clics al CTA de marca, y
contactos / leads generados.

## Consecuencias

**Positivas**

- El rumbo del producto queda claro y medible: cada trabajo se justifica por
  cuánto aprendizaje o cuántos contactos aporta.
- Evita construir monetización cara (pagos, cuentas) sobre demanda no validada.
- Mantiene el costo bajo: seguimos siendo una PWA estática hasta que un dato
  pida más.
- Deja la puerta abierta a monetizar más adelante sin comprometernos hoy con un
  modelo.

**Negativas / trade-offs**

- Exige **instrumentación** (analítica) y una **política de privacidad /
  consentimiento**, que hoy no existen. Salimos del estado "solo estático".
- **Riesgo legal a cuidar:** el juego tiene categoría **+18** (mazo `spicy`) y
  puede alcanzar a **menores**; la captación de datos y el consentimiento deben
  contemplarlo explícitamente.
- Ata el roadmap a métricas de atención/lead-gen; features "lindas" que no
  muevan esas métricas quedan postergadas.
- No genera ingresos directos en el corto plazo; el retorno es indirecto (para
  Sostaina) y depende de tráfico que todavía hay que construir.

## Alternativas consideradas

- **B2B para eventos** — ticket alto, pero requiere un músculo de **ventas** y
  **entrega a medida** que hoy no tenemos. No ahora.
- **B2C freemium** — **ARPU bajo** y **fricción de cobro** alta sobre un juego
  que la gente espera gratis. No ahora.
- **Patrocinio** — oportunista y depende de **tráfico que aún no existe**; sin
  audiencia no hay qué patrocinar. No ahora.
