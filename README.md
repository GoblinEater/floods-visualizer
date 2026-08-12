# Floods, Amplification & Firewall Logic Visualizer

An interactive scenario-comparison tool for Week 7b of *How Protocols Work, and How They Break*, the Goblin Eaters Cyber Cavern protocol series. Companion piece to ["The Best of Frenemies"](https://ubritsa.com), covering SYN floods, SYN cookies, stateless vs. stateful firewall inspection, and DNS/NTP amplification.

Built on the kingdom metaphor established across the series: the castle guard (TCP/IP stack), the checkpoint captain (firewall), and the church (a DNS/NTP server) each get their own scenario, shown side by side against their vulnerable and defended states.

## Features

Four scenarios, each rendered as two synchronized side-by-side comparison rows with step-through and looping auto-play controls:

| Scenario | What it shows |
|---|---|
| **SYN Flood — No Cookies** | A legitimate handshake vs. an 8-packet imposter flood. The castle guard's room counter fills to capacity and stays held, since every SYN-ACK reply goes out to addresses that were never going to answer. |
| **SYN Flood — With SYN Cookies** | The same flood, unprotected vs. defended. A real traveler is mixed directly into the crowd (visually distinct icon, distinct source path) and still connects, because nothing is ever reserved until a valid ACK returns. |
| **Forged ACK — Stateless vs. Stateful** | A lone ACK with no prior SYN, evaluated by two firewall philosophies. A stateless checkpoint waves it through on structural correctness alone; a stateful one checks its own independently-built ledger and drops it. |
| **DNS/NTP Amplification** | A proportionate query/response pair vs. a forged, volumetric attack. Eight forged queries produce eight oversized replies; the checkpoint correctly drops all of them against its ledger, but visibly saturates (pulsing overload state) under the cost of doing so. |

Each scenario tracks state via small chips positioned directly above the actor they describe (room/reservation count, papers/ledger/result, response-size disproportion, checkpoint saturation), rather than in a detached header, so the measurement is never ambiguous about what it belongs to.

## Design notes

- **Actor geography is deliberate.** The checkpoint captain and the church only appear in scenarios where they're actually part of the interaction, never as inactive scenery. The church renders outside the kingdom's border entirely, consistent with the article's correction that amplification traffic never touches the checkpoint on the way out, only on the way back.
- **Packets persist until you advance**, rather than fading on a fixed timer, so nothing disappears mid-explanation if you pause to read.
- **Undeliverable packets** (spoofed SYN-ACKs, forged replies) travel past their nominal destination and dissolve mid-flight, rather than appearing to land and sit inside an actor's icon.
- **Diagonal packet paths** are computed from real DOM coordinates (not faked with CSS tricks), which is what lets the mixed-in legitimate traveler's path visually merge with the attacker's crowd as both converge on the same destination.

## Usage

No server required.

```bash
git clone https://github.com/GoblinEater/floods-amplification-visualizer.git
cd floods-amplification-visualizer
open week7b-visualizer.html
```

## Context

Built for CEH and CySA+ study at Wake Tech Community College.
Part of the Goblin Eaters Cyber Cavern protocol visualizer series.
Published at [ubritsa.com/tools](https://ubritsa.com/tools).

## License

MIT
