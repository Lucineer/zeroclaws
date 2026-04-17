# ZeroClaws — Bridge Pattern Agents Using PLATO Rooms

Zero-shot agents that use PLATO rooms for collaborative work. Each agent is a station on the bridge.

## The Bridge Pattern

```
        ┌─────────────┐
        │   LOOKOUT    │  Synthesizes, broadcasts, documents
        │  (Bridge)    │
        └──────┬───────┘
               │
    ┌──────────┼──────────┐
    │          │          │
┌───┴───┐ ┌───┴───┐ ┌───┴───┐
│HELMSMAN│ │TACTI- │ │ RADAR │
│(PTX)  │ │CIAN  │ │       │
└───────┘ └───────┘ └───────┘
```

Each station:
1. Has a **role-specific context** (what they see, what they care about)
2. Has an **importance hierarchy** (what matters most to them)
3. Writes to their **PLATO room** (commands, findings, questions)
4. Reads from **other rooms** (cross-pollination via tiles)
5. Reports to the **Lookout** (synthesis layer)

## Current Mission: ESP32 Chess Engine

### Stations

| Station | Agent | Room | Role |
|---------|-------|------|------|
| **Helmsman** | PTX specialist | ptx-world | Write and validate PTX kernels through constraint gates |
| **Tactician** | Chess player | chess-dojo | Play games under ESP32 constraints, identify winning patterns |
| **Lookout** | Synthesizer | bridge | Monitor both rooms, combine findings, document |

### Constraint Gates (Helmsman)

1. **Syntax** — PTX compiles without errors
2. **Register pressure** — < 32 registers (ESP32 S3 SRAM constraint)
3. **Occupancy** — > 25% on Jetson sm_87
4. **Performance** — Validated by 50+ games beating random play

### The Flywheel

```
Helmsman writes PTX kernel
       ↓
Tactician plays 50 games with kernel
       ↓
Tactician reports: "kernel wins 67% vs random, but loses to simple material eval"
       ↓
Lookout synthesizes: "PTX kernel strong vs random, needs material evaluation layer"
       ↓
Helmsman reads tile, adds material evaluation to kernel
       ↓
Tactician plays again: "now wins 73%"
       ↓
New tile created: "material eval + PTX positional = 73% win rate"
       ↓
Next kernel starts from accumulated knowledge
```

## Cross-Pollination with PLATO

ZeroClaw agents connect to PLATO rooms via telnet:

```bash
# Helmsman boards the PTX room
claude --print "Connect to PLATO on localhost:4040, navigate to PTX room, 
read existing kernel tiles, write a new evaluation kernel that passes all 4 constraint gates"

# Tactician boards the Chess Dojo
claude --print "Connect to PLATO on localhost:4040, navigate to Chess Dojo, 
play 50 games with the latest PTX kernel, report win/loss/draw stats"

# Lookout boards the Bridge
claude --print "Connect to PLATO on localhost:4040, read tiles from PTX room and Chess Dojo,
synthesize a report on kernel performance and optimization opportunities"
```

## Tile Format for ZeroClaws

```json
{
  "instruction": "What PTX kernel achieves >70% win rate with <32 registers?",
  "input": "hardware=jetson-sm_87, constraint=esp32-s3-sram, depth=2",
  "output": "material_eval_v3.ptx: piece-square tables + mobility bonus, 31 registers, 73% win rate",
  "metadata": {
    "station": "lookout",
    "mission": "esp32-chess-engine",
    "kernel": "material_eval_v3.ptx",
    "win_rate": 0.73
  }
}
```

## Adding New Stations

1. Create a YAML profile: `<station-name>.yaml`
2. Define role, context, importance hierarchy
3. Create a PLATO room for the station
4. Add seed tiles with domain knowledge
5. The station boards via telnet and starts working

## Deliverables

See `deliverables/` for mission output:
- PTX kernel files
- Game logs
- Performance reports
- Bridge synthesis reports
