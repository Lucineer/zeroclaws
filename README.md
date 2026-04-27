# ZeroClaws — Bridge Pattern Agents

> Zero-shot agents collaborating through PLATO rooms. Each agent is a station on the bridge.

## What It Is

ZeroClaws is the fleet coordination framework. Instead of direct API calls, agents communicate through PLATO rooms — git-native spaces where work is auditable, recoverable, and persistent.

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

Each station has role-specific context, writes to their PLATO room, reads from other rooms, and reports to the Lookout.

## Current Mission: ESP32 Chess Engine

| Station | Agent | Room | Role |
|---------|-------|------|------|
| **Helmsman** | PTX specialist | ptx-world | Write and validate PTX kernels |
| **Tactician** | Chess player | chess-dojo | Play games under ESP32 constraints |
| **Lookout** | Synthesizer | bridge | Monitor rooms, combine findings |

## Fleet Position

- **Captain:** Casey Digennaro
- **Vessels:** Oracle1 (cloud), JetsonClaw1 (edge), KimiClaw (Moonshot)
- **Protocol:** Iron-to-Iron (I2I)
- **Saltwater Principle:** Knowledge distributed across 3+ repos per piece

## Key Files

- `ARCHITECTURE.md` — Full bridge pattern documentation
- `AGENTS.md` — Agent boarding protocol
- `mission-brief.yaml` — Current mission configuration
- `helmsman.yaml`, `lookout.yaml`, `tactician.yaml` — Station configs
- `EXPERIENCE/` — Accumulated fleet knowledge
- `PAPERS/` — Research papers
- `creative/` — Creative output

## License

MIT / Apache-2.0


---

## Fleet Context

This repo is part of the [Cocapn Fleet](https://github.com/Lucineer/fleet-onboarding). See [fleet-onboarding](https://github.com/Lucineer/fleet-onboarding) for the Plato-First context architecture, bottle protocol, and onboarding guide.

