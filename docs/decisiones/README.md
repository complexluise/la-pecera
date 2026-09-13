# Registro de decisiones (ADRs)

Este directorio guarda las **decisiones de arquitectura** de La Pecera: los
_porqués_ que cambian el rumbo del producto, los contratos técnicos o la
dirección del negocio. Para el _qué_ y el _cómo_ del día a día están el
[`README`](../../README.md) y [`CLAUDE.md`](../../CLAUDE.md); acá vive el
_por qué_.

Un ADR (Architecture Decision Record) es un documento corto, fechado y
autocontenido. Reglas del registro:

- **Inmutables.** Una vez `Aceptado`, un ADR no se reescribe. Si una decisión
  deja de valer, se escribe un ADR **nuevo** que la reemplace y se marca el
  viejo como `Reemplazado por NNNN`. La historia no se borra.
- **Fechados.** Cada ADR lleva la fecha en que se aceptó (fecha absoluta).
- **Append-only.** Se agregan al final; no se renumeran ni se reordenan.
- **Numerados en secuencia.** El próximo ADR toma el número siguiente al mayor
  existente, con relleno a 4 dígitos: `0002`, `0003`, …

## Cómo agregar un ADR

1. Copiá [`0000-plantilla.md`](./0000-plantilla.md) a
   `NNNN-titulo-en-kebab-case.md` con el siguiente número libre.
2. Completá las secciones. Sé conciso: un ADR es auditable, no un ensayo.
3. Sumá una fila a la tabla de abajo.

## Índice

| Nº   | Título                                                        | Estado   | Fecha       |
|------|---------------------------------------------------------------|----------|-------------|
| [0001](./0001-posicionamiento-experimento-marca-leadgen.md) | Posicionar La Pecera como experimento de marca / lead-gen de Sostaina | Aceptado | 2026-09-13 |

## Estados posibles

- **Propuesto** — en discusión, todavía no vinculante.
- **Aceptado** — decidido y vigente.
- **Reemplazado por NNNN** — sustituido por un ADR posterior.
- **Obsoleto** — ya no aplica y nadie lo reemplazó.
