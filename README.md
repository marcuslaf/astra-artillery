# Astra Artillery

> **Original 2D turn-based artillery web game - v0.2.0**

[![Status](https://img.shields.io/badge/status-v0.2.0-green)]()
[![Next.js](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org/)
[![Phaser](https://img.shields.io/badge/Phaser-3.88-orange)](https://phaser.io/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)](https://www.typescriptlang.org/)
[![Tailwind](https://img.shields.io/badge/Tailwind-3.4-38bdf8)](https://tailwindcss.com/)
[![Tests](https://img.shields.io/badge/tests-246%20passing-brightgreen)]()
[![Vercel](https://img.shields.io/badge/Deploy-Vercel-black)](https://vercel.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Visao Geral / Overview

**Astra Artillery** e um jogo web original de artilharia em turnos, inspirado no genero classico popularizado por jogos como *DDTank*, *Worms* e *Gunbound*.

**Astra Artillery** is an original turn-based artillery web game, inspired on the classic genre popularized by games like *DDTank*, *Worms* and *Gunbound*.

> **Importante / Important**: Este e um projeto **original**. Nao utiliza assets, codigo, personagens, nomes ou qualquer propriedade intelectual de jogos existentes.
> This is an **original** project. It does not use assets, code, characters, names or any intellectual property from existing games.

### Premissa / Premise

O mundo de **Astra** era protegido por cristais de energia chamados **Nucleos Astrais**. Apos **A Grande Ruptura**, os cristais se espalharam por diferentes regioes. Criaturas e faccoes disputam essa energia.

The world of **Astra** was protected by energy crystals called **Astral Cores**. After **The Great Rift**, the crystals spread across different regions. Creatures and factions fight for this energy.

---

## Gameplay

| Funcionalidade / Feature | Descricao / Description |
|--------------------------|------------------------|
| Combate por turnos / Turn-based combat | Calcule angulo, potencia e vento / Calculate angle, power and wind |
| 8 personagens / 8 characters | Kai, Luna, Bolt, Nova, Zephyr, Igneous, Glacis, Aeris |
| 24 fases + 6 boss fights | Across 6 thematic regions |
| IA deterministica / Deterministic AI | 3 niveis de dificuldade / 3 difficulty levels |
| Fisica arcade / Arcade physics | Trajetoria parabolica com vento dinamico / Parabolic trajectory with dynamic wind |
| Terreno destrutivel / Destructible terrain | Deformacao dinamica / Dynamic deformation |
| Save system | Export/import/backup com validacao / with validation |
| i18n | Portugues (BR), English, Espanol |
| PWA | Instalacao offline com update automatico / Offline install with auto update |

### Controles / Controls

| Acao / Action | Desktop | Mobile |
|---------------|---------|--------|
| Mover / Move | A / D or arrows | Touch buttons |
| Mirar / Aim | W / S or arrows | Touch buttons |
| Carregar/Disparar / Charge/Fire | Space (hold/release) | Touch hold |
| Habilidade / Ability | Shift | Touch button |
| Pausar / Pause | ESC / P | Touch button |

Gamepad tambem suportado via Gamepad API / Gamepad also supported via Gamepad API.

---

## Arquitetura / Architecture

`
src/
  app/                    # Next.js App Router
    page.tsx              # Home/Splash
    story/page.tsx        # Narrative intro
    characters/page.tsx   # Character selection
    map/page.tsx          # Stage selection
    game/page.tsx         # Battle (Phaser)
    arsenal/page.tsx      # Projectile arsenal
    training/page.tsx     # Training mode
    missions/page.tsx     # Weekly missions
    profile/page.tsx      # Player profile
    settings/page.tsx     # Full settings
    about/page.tsx        # Credits
  components/
    ui/                   # PageTransition, ReduceMotion, UpdateBanner
    game/                 # HUD, PauseOverlay, ErrorBoundary, mobile controls
    loading/              # GameLoader, LoadingScreen, NavigationLoader
    nav/                  # NavMenu responsivo
  game/                   # Phaser core (isolated from React)
    config/               # Game configurations
    scenes/               # Boot, Preload, Battle, UI
    entities/             # Character, Projectile, Terrain
    systems/              # Turn, Wind, Damage, AI, Camera, Pause, Weather,
                          #   Terrain, Impact, ScreenFlash, Feedback, Rewards
    physics/              # Ballistics
    characters/           # Character registry
    ai/                   # CPU Player
  stores/                 # Zustand (gameStore ~2200 lines)
  hooks/                  # usePhaserGame, useGameControls, useI18n, useSWUpdate
  i18n/                   # 3 locales, 200+ keys
  types/                  # TypeScript definitions
  utils/                  # audio, fullscreen, gamepad, graphicsQuality, storage, math
`

### Separacao de Responsabilidades / Responsibility Separation

| Camada / Layer | Responsabilidade / Responsibility |
|----------------|----------------------------------|
| **Next.js** | Paginas, menus, layout, SEO, UI fora do combate / Pages, menus, layout, SEO, UI outside combat |
| **Phaser** | Game loop, sprites, fisica, trajetoria, colisoes, particulas, terreno / Game loop, sprites, physics, trajectory, collisions, particles, terrain |
| **Zustand** | Configuracoes, progresso, personagem selecionado, estado compartilhado / Settings, progress, selected character, shared state |
| **React** | Bridge para Phaser, controles mobile, HUD overlay, menus / Bridge to Phaser, mobile controls, HUD overlay, menus |

---

## Stack Tecnologica / Tech Stack

| Tecnologia / Technology | Versao / Version | Uso / Purpose |
|-------------------------|------------------|---------------|
| Next.js | 15 (App Router, Server Components) | Framework |
| React | 18 | UI Library |
| TypeScript | 5 | Type safety |
| Phaser | 3.88 | Game Engine 2D |
| Zustand | 5 | Global state |
| Tailwind CSS | 3.4 | Styling |
| Vitest | 2 | Unit tests (246 tests) |
| Playwright | 1.47 | E2E tests |
| ESLint | 9 | Linting |
| Prettier | 3 | Formatting |
| Vercel | - | Deploy |

---

## Instalacao e Execucao / Setup and Running

### Pre-requisitos / Prerequisites

- Node.js 20+
- npm 10+

### Setup

`ash
# Clonar repositorio / Clone repository
git clone <repo-url>
cd astra-artillery

# Instalar dependencias / Install dependencies
npm install

# Instalar browsers do Playwright / Install Playwright browsers
npx playwright install chromium

# Desenvolvimento / Development
npm run dev

# Build de producao / Production build
npm run build

# Iniciar producao / Start production
npm start
`

### Scripts Disponiveis / Available Scripts

| Script | Descricao / Description |
|--------|------------------------|
| 
pm run dev | Servidor de desenvolvimento / Development server |
| 
pm run build | Build para producao / Production build |
| 
pm run start | Servidor de producao / Production server |
| 
pm run lint | ESLint |
| 
pm run typecheck | TypeScript check |
| 
pm run format | Prettier write |
| 
pm run format:check | Prettier check |
| 
pm run test | Vitest (unit tests) |
| 
pm run test:watch | Vitest watch mode |
| 
pm run test:ui | Vitest UI |
| 
pm run test:coverage | Test coverage |
| 
pm run test:e2e | Playwright E2E |
| 
pm run test:e2e:ui | Playwright UI |

---

## Testes / Tests

### Unitarios (Vitest)

246 testes cobrindo / 246 tests covering:
- Utilitarios matematicos (clamp, lerp, distance, etc.) / Math utilities
- Fisica balistica (calculateTrajectory, calculateDamage, vento) / Ballistic physics
- Logica de personagens e habilidades / Character and ability logic
- Dados de recompensas, missoes, achievements / Reward, mission, achievement data
- Validacao de save/load / Save/load validation

### End-to-End (Playwright)

Fluxos testados / Tested flows:
- Home > Iniciar > Selecao personagem > Mapa > Jogo / Home > Start > Character selection > Map > Game
- Configuracoes (toggles, sliders) / Settings
- Sobre (creditos, tecnologias) / About (credits, technologies)

---

## Build e Deploy / Build and Deploy

### Vercel (Recomendado / Recommended)

1. Conecte o repositorio ao Vercel / Connect repository to Vercel
2. Configure variaveis de ambiente (se houver) / Configure env vars (if any)
3. Deploy automatico a cada push na main / Auto deploy on every push to main

`ash
# Verificacoes locais antes do deploy / Local checks before deploy
npm run lint
npm run typecheck
npm run test
npm run build
`

### Variaveis de Ambiente / Environment Variables

`nv
# .env.local (nao commitado / not committed)
NEXT_PUBLIC_GAME_VERSION=0.2.0
`

---

## Funcionalidades / Features

| Feature | Status |
|---------|--------|
| Pausa multi-source (ESC/gamepad/touch) | v0.2.0 |
| Crossfade de musica entre cenas / Crossfade between scenes | v0.2.0 |
| Fullscreen toggle (cross-browser) | v0.2.0 |
| Gamepad support (Gamepad API) | v0.2.0 |
| i18n 3 idiomas / 3 languages (PT/EN/ES) | v0.2.0 |
| Graphics quality (auto/low/medium/high) | v0.2.0 |
| Save validation + auto-backup | v0.2.0 |
| ErrorBoundary global no layout | v0.2.0 |
| Accessibility enforcer (high contrast, large text, reduce motion) | v0.2.0 |
| PWA update banner | v0.2.0 |
| CHANGELOG.md + LICENSE (MIT) | v0.2.0 |

---

## Roadmap

### MVP (v0.1.0)
- [x] Setup do projeto (Next.js + Phaser + Tooling)
- [x] Identidade visual (logo, favicon, brand)
- [x] Loading screen e transicoes
- [x] Historia introdutoria
- [x] 4 personagens com stats e habilidades
- [x] Selecao de personagem responsiva
- [x] Phaser bootstrap (Boot, Preload, Battle, UI scenes)
- [x] 3 arenas estaticas
- [x] Sistema de turnos com vento dinamico
- [x] Input unificado (teclado + touch)
- [x] Balistica arcade + projetil
- [x] Colisao, dano, HP, KO
- [x] Habilidades especiais
- [x] CPU AI (3 dificuldades)
- [x] Progressao LocalStorage
- [x] Audio (music/SFX toggles)
- [x] Mobile (landscape hint, touch areas 44px+)
- [x] Acessibilidade (reduce motion, focus visible, ARIA)
- [x] Testes unitarios + E2E
- [x] Build Vercel ready

### Expansao (v0.2.0)
- [x] 4 novos personagens (Zephyr, Igneous, Glacis, Aeris)
- [x] 21 novas fases + 6 boss fights
- [x] 6 regioes tematicas
- [x] Terreno destrutivel
- [x] Arsenal de projeteis
- [x] Missoes semanais
- [x] Modo treino
- [x] Perfil do jogador
- [x] Sistema de conquistas
- [x] Astra Cores (habilidades passivas)
- [x] New Game+

### Premium (v0.2.0 polish)
- [x] Pausa multi-source
- [x] Crossfade de audio
- [x] Fullscreen toggle
- [x] Gamepad support
- [x] i18n 3 idiomas
- [x] Graphics quality settings
- [x] Save validation + backup
- [x] ErrorBoundary global
- [x] Accessibility enforcement
- [x] PWA update mechanism

### Futuro / Future
- [ ] Multiplayer online (PvP, matchmaking)
- [ ] Mais fases e capitulos / More stages and chapters
- [ ] Leaderboards e rankings
- [ ] Clas/Guildas / Clans/Guilds
- [ ] Replay system

---

## Licenca / License

MIT License - ver [LICENSE](LICENSE).

**Todos os direitos reservados a equipe Astra Artillery.**
**All rights reserved to the Astra Artillery team.**

- Codigo original / Original code
- Assets SVG originais / Original SVG assets
- Game design original / Original game design
- Narrativa original / Original narrative
- Nenhum asset de terceiros (DDTank, Worms, etc.) / No third-party assets

---

## Creditos / Credits

| Funcao / Role | Autor / Author |
|---------------|----------------|
| Game Design | Original |
| Programacao / Programming | TypeScript, React, Next.js, Phaser 3 |
| Arte & UI | SVG Original, CSS/Tailwind |
| Musica & SFX | Placeholders (substituir por originais / replace with originals) |
| QA & Testes / QA & Tests | Vitest (246) + Playwright |

---

*Desenvolvido com amor usando tecnologias web modernas*
*Built with love using modern web technologies*