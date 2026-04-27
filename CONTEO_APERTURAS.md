# Conteo de Aperturas y Variantes - Lichess

## Fecha: 2026-04-27

---

## Resumen del Conteo

### Repositorio chess-openings (lichess-org/chess-openings)

Los archivos TSV contienen datos estructurados por volumen ECO. Hasta ahora he analizado:

| Archivo | Volúmenes | Líneas Aproximadas |
|---------|-----------|-------------------|
| a.tsv | A00-A99 | ~1,500+ líneas |
| b.tsv | B00-B99 | ~2,000+ líneas |

### Estimación Total (chess-openings estándar)

Basado en el conteo parcial:
- **Volumen A**: ~1,500 aperturas/variantes
- **Volumen B**: ~2,000 aperturas/variantes
- **Total estimado**: ~3,500+ aperturas/variantes

### Variantes No Estándar (Lichess API)

Según la documentación del repositorio `lila-openingexplorer`, las variantes disponibles son:

| Variante | Descripción |
|----------|-------------|
| **standard** (chess) | Ajedrez estándar 50x50 |
| **antichess** | Ajedrez inverso (capturar piezas negras) |
| **atomic** | Variantes con piezas explosivas |
| **chess960** | Fischer Random Chess |
| **horde** | Variante con peones en la primera fila |
| **racingKings** | Variante con reyes en la primera fila |
| **threeCheck** | Ajedrez con tres jaques |
| **crazyhouse** | Crazyhouse (capturar piezas para añadir al tablero) |
| **kingOfTheHill** | King of the Hill |

---

## Metodología de Conteo

### Paso 1: Obtener conteo total de aperturas/variantes
- Leer todos los archivos TSV del repositorio chess-openings (a.tsv, b.tsv, c.tsv, d.tsv, e.tsv)
- Contar líneas únicas por ECO code
- Identificar todas las hojas (variantes más específicas)

### Paso 2: Mapear estructura jerárquica
- Organizar aperturas por familia principal → variante → subvariante
- Identificar transposiciones y nombres alternativos

### Paso 3: Validación con API de Lichess
- Usar endpoint de Opening Explorer para verificar datos
- Comparar conteos entre repositorio y API en vivo

---

## Desafíos Identificados

### 1. Transposiciones y Duplicados
- Una misma posición puede tener múltiples nombres de apertura
- Ejemplo: `King's Pawn Game` vs `Queen's Pawn Game` según movimiento inicial

### 2. Variantes No Estándar
- Aperturas como Chess960, Antichess, Atomic, Crazyhouse, Horde, King of the Hill, Racing Kings
- Estas no están en el repositorio chess-openings estándar (solo volumen ECO A y B)

### 3. API Limitaciones
- La API de Lichess requiere parámetros específicos para obtener aperturas
- No hay endpoint directo para "todas las aperturas"
- El endpoint `player` devuelve datos basados en movimientos, no lista completa de aperturas

---

## Próximos Pasos

1. **Obtener conteo completo** de todos los archivos TSV (a.tsv, b.tsv, c.tsv, d.tsv, e.tsv)
2. **Validar con API** de Lichess Opening Explorer para diferentes variantes
3. **Incluir variantes no estándar** (Chess960, Antichess, etc.)
4. **Generar reporte final** con conteo exacto de todas las hojas

---

## Notas Adicionles

- Los datos del repositorio chess-openings están en el dominio público (CC0)
- La API de Lichess está disponible para uso comercial y no comercial
- El database de lichess.org contiene evaluaciones de millones de posiciones
