# Tab Item

Source of truth (Figma): [Ui Kit 1.0 - Tab Item](https://www.figma.com/design/CSTmHAMHrIN2rmnimwjV1z/Ui-Kit-1.0?node-id=10804-133&t=DwumgykElA4LLHvj-4)

Singola tab all'interno di una Tab Bar. Larghezza hug, **max 320px**. Oltre il limite, la label viene troncata con ellipsis (...). Altezza fissa **48px**.

## Content Variants (Ufficiali)

| # | Variant | Elementi |
|---|---------|----------|
| 1 | **Label** | Solo testo — navigation tab semplice |
| 2 | **Swatch + Label** | Pallino colore + testo — identifica un job o documento |
| 3 | **Swatch + Label + Close** | Job chiudibile (variant più frequente) |
| 4 | **Icon + Label + Close** | Contenuto categorizzato chiudibile (info, warning, ecc.) |

> **Attenzione:** Swatch e Icon sono mutuamente esclusivi — non vanno mai usati insieme.

## Stati

| State | Background | Border-bottom | Label color | Note |
|-------|------------|--------------|-------------|------|
| **Default** | — | `transparent` | `color/text/tertiary` `#97999b` | Stato base |
| **Hover** | `rgba(0,0,0,0.04)` | `transparent` | `color/text/tertiary` `#97999b` | |
| **Active** | — | `4px solid color/black/100` `#000` | `color/text/primary` `#000` | Una sola tab attiva alla volta |
| **Disabled** | — | `transparent` | `color/text/tertiary` `#97999b` | `opacity: 0.4`, non interattivo |

## Properties

| Property | Valori | Descrizione |
|----------|--------|-------------|
| `State` | `Default` \| `Hover` \| `Active` \| `Disabled` | Stato visuale della tab |
| `Label` | testo | Testo editabile, troncato con `...` a 320px |
| `Show Swatch` | `true` \| `false` | Mostra pallino colore 16×16 px, radius 4px |
| `Swatch Color` | `rgb(r, g, b)` | Colore pallino — default `rgb(215, 25, 47)` = `color/brand/200` |
| `Show Icon` | `true` \| `false` | Mostra icona Outline 14×14 px |
| `Show Close` | `true` \| `false` | Mostra pulsante `×` di chiusura |

## Struttura Interna

```
[Swatch | Icon]  [Label]  [Close ×]
```

- Auto-layout row, align: center
- `padding-x`: 16px (`spacing/4`)
- `gap`: 8px (`spacing/2`) — 8px anche in Disabled (`radius/md`)
- Slot opzionali collassano automaticamente quando disabilitati
- Label con `text-overflow: ellipsis` quando il contenuto totale supera 320px

## Design Tokens

### Colors

| Token | Valore |
|-------|--------|
| `color/brand/200` | `rgb(215, 25, 47)` — colore swatch di default |
| `color/border/default` | `rgb(230, 230, 230)` — bordo swatch |
| `color/text/primary` | `rgb(0, 0, 0)` — label Active |
| `color/text/tertiary` | `rgb(151, 153, 155)` — label Default/Hover/Disabled |
| `color/black/100` | `rgb(0, 0, 0)` — border-bottom Active |
| `color/icon/primary` | `rgb(0, 0, 0)` |

### Spacing

| Token | Valore | Utilizzo |
|-------|--------|----------|
| `spacing/2` | 8px | Gap tra elementi |
| `spacing/4` | 16px | Padding orizzontale |
| `spacing/12` | 48px | Altezza fissa |

### Radius

| Token | Valore | Utilizzo |
|-------|--------|----------|
| `radius/md` | 8px | Gap in stato Disabled; radius del pallino swatch è 4px |

## Typography

- Font: `Roboto Bold`
- Size: `13px`
- Line-height: `21px`
- Overflow: `ellipsis`, `whitespace: nowrap`

## Do

- Usa una delle 4 varianti ufficiali
- Mantieni una sola tab Active alla volta
- Esprimi sempre il colore dello swatch in formato RGB — `rgb(r, g, b)` con valori 0–255
- Per label lunghe usa un titolo abbreviato (limite 320px fisso)
- Disabilita Close su tab unica o pinnata

## Don't

- Non combinare Swatch + Icon nella stessa tab
- Non superare 320px width / 48px height
- Non usare HEX o HSL per il colore dello swatch — solo RGB
- Non usare icone Filled — solo Outline 14×14
- Non sostituire il colore della border-bottom in stato Active

## Reference CSS

```css
/* Tab Item — container */
display: flex;
flex-direction: row;
align-items: center;
justify-content: center;
padding: 0 16px;       /* spacing/4 */
gap: 8px;              /* spacing/2 */

height: 48px;          /* spacing/12 */
max-width: 320px;

/* border-bottom è sempre presente; solo il colore cambia */
border-bottom: 4px solid transparent;

/* State: Hover */
background: rgba(0, 0, 0, 0.04);

/* State: Active */
border-bottom-color: var(--color\/black\/100, #000000);

/* State: Disabled */
opacity: 0.4;
pointer-events: none;

/* Label */
font-family: 'Roboto', sans-serif;
font-weight: 700;
font-size: 13px;
line-height: 21px;
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
color: var(--color\/text\/tertiary, #97999b); /* Default/Hover/Disabled */
/* color: var(--color\/text\/primary, #000);   Active */
```
