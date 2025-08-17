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
  ▓ LAYOUT (suggested)
  hw-shards/
    obelisk/       → ESP32↔USART bridge + STM32F103 hub logic               [submodule]
    vertex/        → Night-lamp controller (ATmega328P, “СоюзПечаль”)       [submodule]
  ws-shards/
    concentrator/  → A hub to make from websocket a bus                     [submodule]
    luch/          → Telegram interface                                     [submodule]
  servers/                                                                  [depricated]
    tma/           → WebSocket server (pure C), gateway for Obelisk         [submodule]

  ───────────────────────────────────────────────────────────────
  ▓ QUICK START
  # Clone superproject + all submodules:
  git clone --recurse-submodules <THIS_REPO_URL> monolith
  cd monolith

  # If you forgot --recurse-submodules:
  git submodule update --init --recursive

  # Later, to sync to the recorded commits:
  git pull
  git submodule update --init --recursive

  ───────────────────────────────────────────────────────────────
  ▓ DAILY WORKFLOW (commit inside submodule, then bump pointer)
  # 1) Work in a submodule:
  cd devices/obelisk
  # …hack, build, test…
  git checkout -b feat/foo
  git add -A && git commit -m "obelisk: implement foo"
  git push -u origin HEAD

  # 2) Record the new submodule commit in the superproject:
  cd ../../
  git add devices/obelisk
  git commit -m "Bump obelisk to <short-hash> (feat: foo)"
  git push

  ───────────────────────────────────────────────────────────────
  ▓ SUBMODULE MANAGEMENT
  # Add a submodule (tracking main is optional):
  git submodule add -b main <REPO_URL> path/inside/meta
  git commit -m "Add submodule: path/inside/meta" && git push

  # Update one submodule to latest on its tracked branch:
  cd path/inside/meta && git fetch && git checkout main && git pull
  cd ../../ && git add path/inside/meta
  git commit -m "Bump path/inside/meta" && git push

  # Remove a submodule cleanly:
  git submodule deinit -f PATH
  git rm -f PATH
  rm -rf .git/modules/PATH
  git add .gitmodules
  git commit -m "Remove submodule PATH" && git push

  # Configure a submodule to track a branch for --remote:
  git config -f .gitmodules submodule.PATH.branch main
  git add .gitmodules && git commit -m "Track main for PATH"

  ───────────────────────────────────────────────────────────────
  ▓ SYNC EVERYTHING
  # Safe (reproducible): use recorded commits
  git submodule update --init --recursive

  # Float to latest of tracked branches (then commit bumps):
  git submodule update --remote --recursive
  git add -A && git commit -m "Bump all submodules" && git push

  # Power users: fast-forward each submodule manually:
  git submodule foreach '
    git fetch origin &&
    (git rev-parse --verify main >/dev/null 2>&1 && git checkout main || true) &&
    git pull --ff-only || true
  '
  git add -A && git commit -m "FF submodules to latest" && git push

  ───────────────────────────────────────────────────────────────
  ▓ TIPS & PITFALLS
  ▪ Always run `git submodule update --init --recursive` on fresh clones/after pull.
  ▪ Inside a submodule, avoid detached HEAD: `git checkout -b fix/thing` or `git checkout main`.
  ▪ Keep artifacts out of Git; use .gitignore and per-repo build/ or out/.
  ▪ Bump one submodule per commit when possible—simplifies bisects.

  ───────────────────────────────────────────────────────────────
  ▓ FINAL WORDS
  Monolith grows in shards—this superproject keeps them aligned.
  Hack boldly. Pin precisely. Ship reproducibly.

