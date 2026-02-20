███╗   ███╗ ██████╗ ███╗   ██╗ ██████╗ ██╗     ██╗████████╗██╗  ██╗
████╗ ████║██╔═══██╗████╗  ██║██╔═══██╗██║     ██║╚══██╔══╝██║  ██║
██╔████╔██║██║   ██║██╔██╗ ██║██║   ██║██║     ██║   ██║   ███████║
██║╚██╔╝██║██║   ██║██║╚██╗██║██║   ██║██║     ██║   ██║   ██╔══██║
██║ ╚═╝ ██║╚██████╔╝██║ ╚████║╚██████╔╝███████╗██║   ██║   ██║  ██║
╚═╝     ╚═╝ ╚═════╝ ╚═╝  ╚═══╝ ╚═════╝ ╚══════╝╚═╝   ╚═╝   ╚═╝  ╚═╝


  ░▒▓█ Monolith — Superproject █▓▒░
  One repo to rule them all. A pinned, reproducible snapshot of the entire Monolith ecosystem via Git submodules.

  ───────────────────────────────────────────────────────────────
  ▓ OVERVIEW
  This repository aggregates all Monolith parts (devices, firmware, servers, tools)
  as Git submodules. The superproject commit acts as a lockfile: clone this repo
  to get the exact, known-good versions of every component.

  ───────────────────────────────────────────────────────────────
  ▓ LAYOUT
  hw-shards/
    obelisk/       → ESP32↔USART bridge + STM32F103 hub logic               [depricated | submodule]
    vertex/        → Night-lamp controller (ATmega328P, “СоюзПечаль”)       [submodule]
  ws-shards/
    concentrator/  → A hub to make from websocket a bus                     [submodule]
    luch/          → Telegram interface                                     [submodule]
    vox/           → Voice control system                                   [submodule]
    achtung/       → Manager of alarms and timers                           [submodule]
    governor/      → Manager of schedule and deadlines                      [submodule]
  servers/                                                                  
    tma/           → WebSocket server, gateway for Obelisk                  [depricated | submodule]

  ───────────────────────────────────────────────────────────────

