# Investigación: Árbol Completo de Aperturas de Ajedrez (Lichess)

## Fecha de Inicio: 2026-04-27

---

## Resumen Ejecutivo

Esta investigación busca identificar y documentar **todas las aperturas y variantes existentes** en el árbol de ajedrez de Lichess, incluyendo todas las hojas del sistema.

### Objetivo Principal
Obtener un conteo exacto de **todas las aperturas/variantes (hojas)** del árbol database de lichess.

---

## Fuentes de Datos Investigadas

### 1. Repositorio GitHub: `lichess-org/chess-openings`
- **URL**: https://github.com/lichess-org/chess-openings
- **Descripción**: Conjunto agregado de nombres de apertura de ajedrez
- **Formato**: Archivos TSV (a.tsv, b.tsv, c.tsv, d.tsv, e.tsv) correspondientes a volúmenes ECO

### 2. API de Lichess Opening Explorer
- **URL**: https://explorer.lichess.ovh/
- **Endpoint**: `https://explorer.lichess.ovh/player?player=foo&color=white&play=e2e4`
- **Licencia**: GNU Affero General Public License v3

### 3. Database de Lichess
- **URL**: https://database.lichess.org/
- **Contenido**: 
  - `lichess_db_eval.jsonl.zst`: 369,477,725 posiciones evaluadas con Stockfish
  - `lichess_db_puzzle.csv.zst`: 5,882,680 puzzles con etiquetas de apertura

---

## Estructura de Datos (chess-openings)

### Campos en archivos TSV:
| Campo | Descripción | Ejemplo |
|-------|-------------|---------|
| `eco` | Clasificación ECO | A00, B00, C00... |
| `name` | Nombre de apertura en inglés | Amar Opening, Bird Opening... |
| `pgn` | Secuencia de movimientos PGN | 1. Nh3 d5 2. g3 e5... |

### Volúmenes ECO:
- **a.tsv**: Volumen A (A00-A99) - Aperturas con peón inicial en h3, a3, b4, c4, d4, e4, f4, g4
- **b.tsv**: Volumen B (B00-B99) - Defensa de peón blanco en e4

---

## Metodología de Investigación

### Paso 1: Obtener conteo total de aperturas/variantes
- Leer todos los archivos TSV del repositorio chess-openings
- Contar líneas únicas por ECO code
- Identificar todas las hojas (variantes más específicas)

### Paso 2: Mapear estructura jerárquica
- Organizar aperturas por familia principal → variante → subvariante
- Identificar transposiciones y nombres alternativos

### Paso 3: Validación con API de Lichess
- Usar endpoint de Opening Explorer para verificar datos
- Comparar conteos entre repositorio y API en vivo

---

## Avances Recientes

### Datos Obtenidos (a.tsv):
- **Formato**: `eco\tname\tpgn`
- **Ejemplo**: 
  ```
  A00	Amar Opening	1. Nh3
  A00	Amar Opening: Paris Gambit	1. Nh3 d5 2. g3 e5 3. f4
  A00	Barnes Opening: Fool's Mate	1. f3 e5 2. g4 Qh4#
  ```

### Datos Obtenidos (b.tsv):
- **Formato**: `eco\tname\tpgn`
- **Ejemplo**: 
  ```
  B00	Barnes Defense	1. e4 f6
  B00	Borg Defense: Borg Gambit	1. e4 g5 2. d4 Bg7
  B00	King's Pawn Game	1. e4
  ```

---

## Desafíos Identificados

### 1. Transposiciones y Duplicados
- Una misma posición puede tener múltiples nombres de apertura
- Ejemplo: `King's Pawn Game` vs `Queen's Pawn Game` según movimiento inicial

### 2. Variantes No Estándar
- Aperturas como Chess960, Antichess, Atomic, Crazyhouse, Horde, King of the Hill, Racing Kings
- Estas no están en el repositorio chess-openings estándar

### 3. API Limitaciones
- La API de Lichess requiere parámetros específicos para obtener aperturas
- No hay endpoint directo para "todas las aperturas"

---

## Próximos Pasos

1. **Obtener conteo completo** de todos los archivos TSV (a.tsv, b.tsv, c.tsv, d.tsv, e.tsv)
2. **Validar con API** de Lichess Opening Explorer
3. **Incluir variantes no estándar** (Chess960, Antichess, etc.)
4. **Generar reporte final** con conteo exacto de todas las hojas

---

## Notas Adicionles

- Los datos del repositorio chess-openings están en el dominio público (CC0)
- La API de Lichess está disponible para uso comercial y no comercial
- El database de lichess.org contiene evaluaciones de millones de posiciones
