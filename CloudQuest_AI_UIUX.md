# CloudQuest AI — Complete UI/UX Design Document
### Version 1.0 | Principal Product Architect | June 2026

---

> **Design Philosophy**
> Every pixel in CloudQuest AI should feel like you are inside the universe you are learning.
> Dark. Dense. Alive. Technical beauty meets gamified depth.

---

## Table of Contents

1. [Design System](#1-design-system)
2. [Sitemap](#2-sitemap)
3. [Navigation Flow](#3-navigation-flow)
4. [Dashboard Design](#4-dashboard-design)
5. [Mission Select Screen](#5-mission-select-screen)
6. [3D Simulator Screen](#6-3d-simulator-screen)
7. [X-Ray Mode Overlay](#7-x-ray-mode-overlay)
8. [XP System Design](#8-xp-system-design)
9. [Achievement Screen](#9-achievement-screen)
10. [User Profile Screen](#10-user-profile-screen)
11. [AI Mentor Interface](#11-ai-mentor-interface)
12. [Mobile Responsive Layout](#12-mobile-responsive-layout)

---

## 1. Design System

### 1.1 Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--color-bg-primary` | `#080C14` | Main background (deep space black) |
| `--color-bg-surface` | `#0D1422` | Card/panel backgrounds |
| `--color-bg-elevated` | `#111827` | Modals, dropdowns |
| `--color-bg-overlay` | `#0A1628` | Sidebar, nav |
| `--color-accent-primary` | `#00D9FF` | Primary CTA, active states (electric cyan) |
| `--color-accent-secondary` | `#7C3AED` | Secondary actions, XP (deep violet) |
| `--color-accent-success` | `#00FF88` | Healthy pods, success states (neon green) |
| `--color-accent-warning` | `#FFB800` | Pending states, warnings (amber) |
| `--color-accent-danger` | `#FF3B6B` | Failed pods, errors, chaos (hot red) |
| `--color-accent-gateway` | `#FF6B35` | Gateway API elements (orange) |
| `--color-accent-storage` | `#A78BFA` | Storage elements (lavender) |
| `--color-text-primary` | `#F0F6FF` | Primary text |
| `--color-text-secondary` | `#7A8BA8` | Secondary/muted text |
| `--color-text-disabled` | `#3A4A5C` | Disabled states |
| `--color-border-subtle` | `#1C2A3D` | Subtle borders |
| `--color-border-active` | `#00D9FF33` | Active/focus borders (translucent cyan) |
| `--color-xp-gold` | `#FFD700` | XP indicators, level badges |

### 1.2 Typography

| Role | Font | Weight | Size |
|---|---|---|---|
| Display / Hero | Outfit | 800 | 48–72px |
| Heading 1 | Outfit | 700 | 32–40px |
| Heading 2 | Outfit | 600 | 24–28px |
| Heading 3 | Inter | 600 | 18–20px |
| Body | Inter | 400 | 14–16px |
| Caption / Label | Inter | 500 | 11–13px |
| Code / YAML | JetBrains Mono | 400 | 13px |
| XP Numbers | Outfit | 800 | varies |

### 1.3 Spacing System (8px base)

```
4px   → xs  (tight gaps, icon padding)
8px   → sm  (component inner padding)
16px  → md  (standard spacing)
24px  → lg  (section spacing)
32px  → xl  (card padding)
48px  → 2xl (section dividers)
64px  → 3xl (hero spacing)
```

### 1.4 Component Library

| Component | Variants |
|---|---|
| Button | Primary (cyan), Secondary (outlined), Ghost, Danger, XP (gold) |
| Card | Default, Elevated, Mission, Achievement, Stat |
| Badge | Level tier, Module tag, Status (Running/Pending/Failed) |
| Progress Bar | XP bar, Mission progress, Skill bar |
| Input | Text, YAML editor, Search |
| Tooltip | Info, Warning, X-Ray callout |
| Modal | Confirmation, Mission briefing, Achievement unlock |
| Panel | Side panel, Bottom panel, Inspector panel |
| Avatar | User avatar, AI Mentor avatar |
| Chip | Tag, Filter, Status |

### 1.5 Motion Design

| Motion | Duration | Easing | Usage |
|---|---|---|---|
| Micro-interaction | 100–150ms | ease-out | Hover, focus |
| Page transition | 300ms | cubic-bezier(0.4, 0, 0.2, 1) | Route change |
| Panel slide | 250ms | ease-in-out | Sidepanel open/close |
| XP animation | 600ms | spring | XP counter increment |
| Achievement unlock | 1200ms | custom spring | Badge pop |
| 3D camera move | 800ms | ease-in-out | Object focus |
| Particle flow | continuous | linear | Network packets |

---

## 2. Sitemap

```
cloudquest.ai/
│
├── /                          → Landing Page
├── /auth
│   ├── /login                 → Login Screen
│   ├── /signup                → Sign Up Screen
│   └── /onboarding            → Persona Quiz
│
├── /dashboard                 → Main Dashboard (Home)
│
├── /learn                     → Learning Path Map
│   ├── /learn/modules         → Module Overview Grid
│   └── /learn/track/:id       → Active Learning Track
│
├── /mission
│   ├── /mission/:id           → Mission Briefing
│   └── /mission/:id/play      → 3D Simulator Screen (full-screen)
│
├── /sandbox                   → Free-form Sandbox Mode
│
├── /chaos-lab                 → Chaos/Failure Simulation Hub
│
├── /xray                      → X-Ray Mode (overlay on simulator)
│
├── /achievements              → Achievements Gallery
│
├── /leaderboard               → Leaderboard Hub
│   ├── /leaderboard/global    → Global Leaderboard
│   ├── /leaderboard/module    → Module Leaderboard
│   └── /leaderboard/friends   → Friends Leaderboard
│
├── /profile
│   ├── /profile/:username     → Public Profile
│   └── /profile/me            → My Profile
│
├── /skill-tree                → Skill Tree Visualization
│
├── /certifications            → Cert Prep Hub (CKA/CKAD/CKS)
│
├── /community
│   ├── /community/missions    → Community Missions
│   └── /community/replays     → Shared Replays
│
└── /settings
    ├── /settings/account      → Account Settings
    ├── /settings/appearance   → Theme / Cosmetics
    └── /settings/org          → Org/Enterprise Settings
```

---

## 3. Navigation Flow

### 3.1 Primary Navigation (Left Sidebar — Collapsed by default on simulator)

```
┌─────────────────────┐
│  ⚡ CloudQuest AI   │  ← Logo + wordmark
├─────────────────────┤
│                     │
│  🏠  Dashboard      │  ← Active state: cyan left border
│  🗺  Learning Path  │
│  🎮  Missions       │
│  🧪  Sandbox        │
│  💀  Chaos Lab      │
│  🏆  Achievements   │
│  📊  Leaderboard    │
│  🌐  Community      │
│                     │
├─────────────────────┤
│  🎓  Cert Prep      │
│  🌳  Skill Tree     │
├─────────────────────┤
│                     │
│  [Avatar]           │
│  Kai Ramirez        │
│  Lv.14 Navigator    │
│  ██████░░ 3,240 XP  │
│                     │
│  ⚙  Settings       │
└─────────────────────┘
```

### 3.2 Top Navigation Bar

```
┌──────────────────────────────────────────────────────────────────────────┐
│  [≡] CloudQuest AI    [Module 3 ▶ Networking]     🔥 7d  ⚡ 3,240 XP  [🔔] [👤] │
└──────────────────────────────────────────────────────────────────────────┘
     ↑                        ↑                       ↑
  Hamburger             Breadcrumb               Streak + XP + Notifications
```

### 3.3 User Journey Flow Diagram

```
[Landing Page]
      │
      ▼
[Sign Up / Login]
      │
      ▼
[Onboarding Quiz] ──── 5 questions ────► [Persona Assigned]
      │                                         │
      ▼                                         ▼
[Dashboard] ◄─────────────────────────── [Track Recommended]
      │
      ├──► [Learning Path Map]
      │           │
      │           ▼
      │    [Module Overview]
      │           │
      │           ▼
      │    [Mission Briefing] ──► [3D Simulator] ──► [Mission Complete]
      │                                │                     │
      │                          [AI Mentor]           [XP Awarded]
      │                          [X-Ray Mode]          [Achievement?]
      │                          [Chaos Lab]            [Debrief]
      │
      ├──► [Sandbox Mode] ──────────────────────────────────────┐
      │                                                          │
      ├──► [Chaos Lab] ─────────────────────────────────────────┤
      │                                                          │
      ├──► [Achievements] ──────────────────────────────────────┤
      │                                                          │
      ├──► [Leaderboard] ──────────────────────────────────────►│
      │                                                          │
      └──► [Profile] ◄───────────────────────────────────────────┘
```

---

## 4. Dashboard Design

### 4.1 Full Dashboard Wireframe (1440px Desktop)

```
┌────────────────────────────────────────────────────────────────────────────────────────────────┐
│  TOP NAV: [≡ CloudQuest AI]                          [🔥 7d Streak]  [⚡ 3,240 XP]  [🔔] [👤]  │
├──────────┬─────────────────────────────────────────────────────────────────────────────────────┤
│          │                                                                                      │
│  SIDE    │   WELCOME BACK BANNER                                                               │
│  NAV     │  ┌───────────────────────────────────────────────────────────────────────────────┐ │
│          │  │  🌌 [Animated starfield / subtle cluster bg]                                  │ │
│  🏠 Home │  │                                                                               │ │
│  🗺 Path │  │  Good evening, Kai  ⚡                                                        │ │
│  🎮 Miss │  │  You're Level 14 — Navigator                                                  │ │
│  🧪 Sand │  │  3,240 / 5,000 XP to Level 15                                                │ │
│  💀 Chaos│  │  ████████████████░░░░░░░░░░░  64%                                             │ │
│  🏆 Ach  │  │                                                                               │ │
│  📊 LB   │  │  [▶ Resume Mission]  [🗺 View Learning Path]                                  │ │
│  🌐 Comm │  │  "Module 3 · Mission 5: Trace the DNS Query"                                  │ │
│          │  └───────────────────────────────────────────────────────────────────────────────┘ │
│  ─────── │                                                                                      │
│  🎓 Cert │   STATS ROW                                                                          │
│  🌳 Tree │  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌──────────────┐              │
│          │  │  🎯 Missions  │ │  🔥 Streak   │ │  🏆 Badges   │ │  📊 Rank     │              │
│  ─────── │  │              │ │              │ │              │ │              │              │
│  [Avatar]│  │     47       │ │   7 Days     │ │     23       │ │   #1,204     │              │
│  Kai R.  │  │  completed   │ │   current    │ │   earned     │ │   Global     │              │
│  Lv.14   │  └──────────────┘ └──────────────┘ └──────────────┘ └──────────────┘              │
│  3240 XP │                                                                                      │
│  ⚙ Sett │   TWO COLUMN LAYOUT                                                                  │
└──────────┤                                                                                      │
           │  ┌────────────────────────────────────────┐  ┌──────────────────────────────────┐  │
           │  │  CONTINUE LEARNING                     │  │  TODAY'S CHALLENGE               │  │
           │  │  ─────────────────────────────────     │  │  ────────────────────────────    │  │
           │  │  Module 3: Networking Internals         │  │  🏁 Daily Mission                │  │
           │  │  ████████████░░░░░░░  Mission 5/25     │  │  "Fix the Broken Service"        │  │
           │  │                                         │  │  ⏱ ~15 min  ·  ⚡ 250 XP        │  │
           │  │  ┌─────────────────────────────────┐   │  │                                  │  │
           │  │  │ 🔴 M3-5: Trace the DNS Query    │   │  │  [▶ Start Challenge]             │  │
           │  │  │ ⏱ ~25 min  ·  ⚡ 300 XP         │   │  │                                  │  │
           │  │  │ [▶ Resume]                       │   │  │  ──────────────────────────────  │  │
           │  │  └─────────────────────────────────┘   │  │  WEEKLY CHALLENGE                │  │
           │  │                                         │  │  🏆 "Chaos: etcd Quorum Loss"    │  │
           │  │  ┌─────────────────────────────────┐   │  │  Ends in: 2d 14h 33m             │  │
           │  │  │ ⬜ M3-6: kube-proxy iptables     │   │  │  Participants: 4,201             │  │
           │  │  │ ⏱ ~30 min  ·  ⚡ 350 XP         │   │  │  Your rank: #847                 │  │
           │  │  │ [🔒 Locked]                      │   │  │  [▶ Join Challenge]              │  │
           │  │  └─────────────────────────────────┘   │  └──────────────────────────────────┘  │
           │  └────────────────────────────────────────┘                                         │
           │                                                                                      │
           │  ┌────────────────────────────────────────┐  ┌──────────────────────────────────┐  │
           │  │  SKILL RADAR                           │  │  RECENT ACHIEVEMENTS             │  │
           │  │  ──────────────────────────────────    │  │  ────────────────────────────    │  │
           │  │                                         │  │                                  │  │
           │  │       Networking ●                      │  │  🥇 "DNS Wizard"      2h ago     │  │
           │  │      /            \                     │  │     Resolved DNS 10x             │  │
           │  │   Security ●    ● Storage               │  │                                  │  │
           │  │      \            /                     │  │  🥈 "No-Hinter"       1d ago     │  │
           │  │       ●──────────●                      │  │     5 missions, no hints         │  │
           │  │   Gateway API   Ops                     │  │                                  │  │
           │  │                                         │  │  🔒 ??? Secret           ?????   │  │
           │  │  [View Full Skill Tree →]               │  │                                  │  │
           │  └────────────────────────────────────────┘  │  [View All Achievements →]       │  │
           │                                              └──────────────────────────────────┘  │
           │                                                                                      │
           │  LEADERBOARD PREVIEW                                                                 │
           │  ┌───────────────────────────────────────────────────────────────────────────────┐ │
           │  │  🏆 This Week's Top Learners                    [View Full Leaderboard →]     │ │
           │  │  ────────────────────────────────────────────────────────────────────────     │ │
           │  │  #1  ██ Arjun M.      Lv.42 Architect    12,400 XP  ████████████████████     │ │
           │  │  #2  ██ Sofia K.      Lv.38 Architect     9,800 XP  ████████████████░░░░     │ │
           │  │  #3  ██ James T.      Lv.35 Engineer      8,200 XP  ████████████░░░░░░░░     │ │
           │  │  ──────────────────────────────────────────────────────────────────────────   │ │
           │  │ #847  ██ You (Kai R.) Lv.14 Navigator     3,240 XP  ██████░░░░░░░░░░░░░░     │ │
           │  └───────────────────────────────────────────────────────────────────────────────┘ │
           │                                                                                      │
           └──────────────────────────────────────────────────────────────────────────────────────┘
```

### 4.2 Dashboard Interaction States

| Element | Default | Hover | Active |
|---|---|---|---|
| Continue Learning card | Dim glow | Cyan border pulse | Scale 1.02 |
| Stats cards | Static | Subtle lift + shadow | — |
| Daily Challenge | Orange border | Intensify border | — |
| Leaderboard row (user) | Highlighted bg | — | — |
| Mission card (locked) | Grayed out, lock icon | Tooltip: "Complete M3-4 first" | — |

---

## 5. Mission Select Screen

### 5.1 Module Overview Grid (Learning Path)

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  TOP NAV                                                                                │
├──────────┬──────────────────────────────────────────────────────────────────────────────┤
│  SIDEBAR │                                                                              │
│          │   LEARNING PATH                                                              │
│          │   ─────────────────────────────────────────────────────────────────          │
│          │   Track: Zero to CKA  ·  Week 5 of 12  ·  ████████░░░░  67% complete        │
│          │                                                                              │
│          │   [Grid View ≡]  [Path View →]         🔍 Search missions...                │
│          │                                                                              │
│          │  ┌────────────────────────────────────────────────────────────────────────┐ │
│          │  │                                                                        │ │
│          │  │  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐             │ │
│          │  │  │  MODULE 1    ✅│  │  MODULE 2    ✅│  │  MODULE 3    🔵│             │ │
│          │  │  │ Cluster Genesis│  │   Workloads   │  │  Networking   │             │ │
│          │  │  │               │  │               │  │               │             │ │
│          │  │  │  18/18 ✅     │  │  22/22 ✅     │  │  5/25 ⬤⬤⬤⬤⬤○○ │             │ │
│          │  │  │  ████████████ │  │  ████████████ │  │  ██░░░░░░░░░░ │             │ │
│          │  │  │               │  │               │  │               │             │ │
│          │  │  │  ⚡ 2,000 XP  │  │  ⚡ 3,500 XP  │  │  ⚡ 5,000 XP  │             │ │
│          │  │  │  [Completed]  │  │  [Completed]  │  │  [Continue▶]  │             │ │
│          │  │  └───────────────┘  └───────────────┘  └───────────────┘             │ │
│          │  │                                                                        │ │
│          │  │  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐             │ │
│          │  │  │  MODULE 4    🔒│  │  MODULE 5    🔒│  │  MODULE 6    🔒│             │ │
│          │  │  │  Gateway API  │  │    Storage    │  │   Security    │             │ │
│          │  │  │               │  │               │  │               │             │ │
│          │  │  │  0/24         │  │  0/20         │  │  0/22         │             │ │
│          │  │  │  ░░░░░░░░░░░░ │  │  ░░░░░░░░░░░░ │  │  ░░░░░░░░░░░░ │             │ │
│          │  │  │               │  │               │  │               │             │ │
│          │  │  │  ⚡ 6,000 XP  │  │  ⚡ 4,500 XP  │  │  ⚡ 5,500 XP  │             │ │
│          │  │  │  [🔒 Locked]  │  │  [🔒 Locked]  │  │  [🔒 Locked]  │             │ │
│          │  │  └───────────────┘  └───────────────┘  └───────────────┘             │ │
│          │  │                                                                        │ │
│          │  └────────────────────────────────────────────────────────────────────────┘ │
└──────────┴──────────────────────────────────────────────────────────────────────────────┘
```

### 5.2 Mission List Within Module

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  ← Back to Modules   MODULE 3: Networking Internals                                    │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                          │
│  [Module header: animated network particle banner]                                       │
│  Understand how Kubernetes networking really works — from ClusterIP to CoreDNS.          │
│  Progress: 5/25 missions  ·  ⚡ 850/5,000 XP earned  ·  ████░░░░░░░░░░  20%            │
│                                                                                          │
│  Filter: [All] [Fix-It] [Build-It] [Investigate] [X-Ray] [Race] [Defend]               │
│                                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐   │
│  │  ✅ 3.1 · INVESTIGATE · ClusterIP: How Virtual IP Works          ⚡ 150 XP ★★★   │   │
│  │  Completed in 18m · Score: 94%  ·  [Replay]                                     │   │
│  └──────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐   │
│  │  ✅ 3.2 · BUILD-IT · NodePort: External Access Basics            ⚡ 180 XP ★★★   │   │
│  │  Completed in 22m · Score: 88%  ·  [Replay]                                     │   │
│  └──────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐   │
│  │  🔵 3.5 · BUILD-IT · NetworkPolicy: Namespace Isolation          ⚡ 280 XP ★★★★  │   │  ← CURRENT
│  │  In Progress · Last attempt: 2h ago  ·  [▶ Resume]                              │   │
│  └──────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐   │
│  │  ⬜ 3.6 · FIX-IT · Pod Can't Talk to Service                     ⚡ 300 XP ★★★★  │   │  ← NEXT
│  │  ~30 min estimated  ·  Prerequisites: 3.5  ·  [▶ Start]                         │   │
│  └──────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                          │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐   │
│  │  🔒 3.10 · X-RAY · Trace a Request from Client to Pod            ⚡ 400 XP ★★★★★ │   │  ← LOCKED
│  │  Requires: 3.9 complete  ·  [🔒 Locked]                                         │   │
│  └──────────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                          │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

### 5.3 Mission Briefing Screen

```
┌────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                                │
│   ← Back   |   Mission 3.6: "Pod Can't Talk to Service"   |   ⚡ 300 XP  ·  ★★★★  ·  ~30min  │
│                                                                                                │
│  ┌────────────────────────────────────────┐   ┌──────────────────────────────────────────┐    │
│  │                                        │   │  OBJECTIVES                              │    │
│  │  [Animated 3D Thumbnail — small        │   │  ─────────────────────────────────────   │    │
│  │   cluster preview showing broken       │   │                                          │    │
│  │   service connection with red X]       │   │  1. ⬜ Identify the misconfigured        │    │
│  │                                        │   │        NetworkPolicy                     │    │
│  │  TYPE: FIX-IT                          │   │  2. ⬜ Fix the policy to allow           │    │
│  │  MODULE: 3 — Networking Internals      │   │        frontend → backend traffic        │    │
│  │                                        │   │  3. ⬜ Verify with curl test             │    │
│  └────────────────────────────────────────┘   │  4. ⬜ Confirm no unintended             │    │
│                                               │        traffic is allowed                │    │
│  STORY BRIEFING                               │                                          │    │
│  ─────────────────────────────────────────    │  RESOURCES PROVIDED                      │    │
│  🚨 Incident Report — 14:32 UTC               │  ─────────────────────────────────────   │    │
│                                               │  • 3-node cluster (pre-configured)      │    │
│  The frontend team is reporting that their    │  • frontend-deploy (3 replicas)          │    │
│  React app can't reach the backend API.       │  • backend-deploy (2 replicas)           │    │
│  Customer orders are failing. The cluster     │  • backend-svc (ClusterIP)               │    │
│  looks healthy on the surface but             │  • NetworkPolicy: deny-all (applied)     │    │
│  something in the NetworkPolicy config        │  • kubectl access                        │    │
│  is blocking traffic.                         │                                          │    │
│                                               │  REWARDS                                 │    │
│  Your job: diagnose and fix the policy        │  ─────────────────────────────────────   │    │
│  before the SLA breach window closes.         │  ⚡ 300 XP (base)                        │    │
│                                               │  🎯 +50% if no hints used                │    │
│                                               │  ⚡ +25% if top 10% speed                │    │
│                                               │                                          │    │
│                                               └──────────────────────────────────────────┘    │
│                                                                                                │
│  ┌──────────────────────────────────────────────────────────────────────────────────────────┐ │
│  │  TIPS FROM YOUR MENTOR  🤖                                                              │ │
│  │  "Before diving in — what does a NetworkPolicy's `podSelector` actually select for?"    │ │
│  └──────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                │
│                           [▶ LAUNCH MISSION]          [📋 View Prerequisites]                 │
│                                                                                                │
└────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 6. 3D Simulator Screen

### 6.1 Full Simulator Layout (1440px)

```
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  TOP HUD BAR                                                                                     │
│  [← Exit]  Mission 3.6: "Pod Can't Talk to Service"  │  ⏱ 12:34  │  ⚡ 300 XP  │  [🤖 Mentor] │
│  ──────────────────────────────────────────────────────────────────────────────────────────────  │
│  Objectives: [1⬜] [2⬜] [3⬜] [4⬜]                    [X-Ray ▼] [Speed: 1x ▼] [Reset]          │
├──────────────────────────────────────────────────────────────────┬───────────────────────────────┤
│                                                                  │                               │
│   3D VIEWPORT (WebGL / Three.js)                                 │  RIGHT PANEL                  │
│                                                                  │                               │
│                                                                  │  ┌─────────────────────────┐  │
│    [CONTROL PLANE — elevated platform, glowing]                  │  │  OBJECT INSPECTOR       │  │
│    ┌──────┐  ┌──────────┐  ┌───────┐  ┌────┐                    │  │  ─────────────────────  │  │
│    │ API  │  │Scheduler │  │  CM   │  │etcd│                    │  │  NetworkPolicy          │  │
│    │Server│  │[animated]│  │[gears]│  │[💎]│                    │  │  deny-all               │  │
│    └──────┘  └──────────┘  └───────┘  └────┘                    │  │                         │  │
│                                                                  │  │  namespace: default      │  │
│   ─────────────────────────────────────────────────             │  │  podSelector: {}         │  │
│                                                                  │  │  policyTypes:            │  │
│    NODE 1                NODE 2               NODE 3             │  │    - Ingress             │  │
│   ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │  │    - Egress              │  │
│   │ [server rack]│  │ [server rack]│  │ [server rack]│          │  │                         │  │
│   │              │  │              │  │              │          │  │  ingress: []  ← empty!  │  │
│   │ 🟢 front-1   │  │ 🟢 front-2   │  │ 🔴 back-1    │          │  │  egress: []             │  │
│   │ 🟢 front-3   │  │ 🟢 back-2    │  │              │          │  │                         │  │
│   │              │  │              │  │              │          │  │  [Edit YAML]            │  │
│   └──────────────┘  └──────────────┘  └──────────────┘          │  │  [Delete]               │  │
│                                                                  │  └─────────────────────────┘  │
│    [RED DASHED LINE between frontend pods and backend pods]      │                               │
│    [🚫 icon floating on broken connection]                       │  ┌─────────────────────────┐  │
│                                                                  │  │  RESOURCE LIST          │  │
│    SERVICES (floating labels above nodes)                        │  │  ─────────────────────  │  │
│    ○ backend-svc ────────────── [🔴 no endpoints reachable]      │  │  📦 Pods (5)            │  │
│                                                                  │  │  🔄 Services (2)        │  │
│                                                                  │  │  🛡 NetworkPolicies (1) │  │
│                                                                  │  │  🗂 Namespaces (1)      │  │
│                                                                  │  └─────────────────────────┘  │
│                                                                  │                               │
│                                                                  │  ┌─────────────────────────┐  │
│    [Floating action: Click any object to inspect]                │  │  YAML EDITOR            │  │
│    [Camera: orbit drag  |  scroll zoom  |  R to reset]           │  │  ─────────────────────  │  │
│                                                                  │  │  apiVersion: network... │  │
│                                                                  │  │  kind: NetworkPolicy    │  │
│                                                                  │  │  spec:                  │  │
│                                                                  │  │    podSelector: {}      │  │
│                                                                  │  │    ingress:             │  │
│                                                                  │  │      - from:            │  │
│                                                                  │  │        [cursor here]    │  │
│                                                                  │  │                         │  │
│                                                                  │  │  [Apply Changes ▶]      │  │
│                                                                  │  └─────────────────────────┘  │
├──────────────────────────────────────────────────────────────────┴───────────────────────────────┤
│  BOTTOM EVENT LOG                                                                                │
│  ┌──────────────────────────────────────────────────────────────────────────────────────────┐   │
│  │  [Events]  [kubectl]  [AI Hints]                                                         │   │
│  │  12:31 ⚠  NetworkPolicy/deny-all applied to namespace default                           │   │
│  │  12:31 ⚠  Endpoints for backend-svc: 0 ready (2 not ready due to NetworkPolicy)         │   │
│  │  12:32 ✗  Connection refused: frontend-1 → backend-svc:8080                             │   │
│  │  12:33 ✗  Connection refused: frontend-2 → backend-svc:8080                             │   │
│  └──────────────────────────────────────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### 6.2 Mission Completion Overlay

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   [Full-screen confetti + particle burst animation]              │
│                                                                  │
│   ╔══════════════════════════════════════════════════════════╗   │
│   ║                                                          ║   │
│   ║         ✅  MISSION COMPLETE!                            ║   │
│   ║                                                          ║   │
│   ║   "Pod Can't Talk to Service"                           ║   │
│   ║                                                          ║   │
│   ║   Score: 94%      Time: 22:18      Rank: Top 8%         ║   │
│   ║                                                          ║   │
│   ║   ─────────────────────────────────────────────────     ║   │
│   ║                                                          ║   │
│   ║   XP BREAKDOWN:                                          ║   │
│   ║   Base XP:          +300 ⚡                              ║   │
│   ║   No-Hint Bonus:    +150 ⚡  (50%)                       ║   │
│   ║   Speed Bonus:      +75  ⚡  (25%)                       ║   │
│   ║                     ─────────                            ║   │
│   ║   TOTAL:           +525  ⚡  [animated counter]          ║   │
│   ║                                                          ║   │
│   ║   ─────────────────────────────────────────────────     ║   │
│   ║                                                          ║   │
│   ║   🏆 ACHIEVEMENT UNLOCKED!                               ║   │
│   ║   "Policy Enforcer" — Fix your first NetworkPolicy       ║   │
│   ║   [badge animation pops in]                              ║   │
│   ║                                                          ║   │
│   ║   LEVEL PROGRESS                                         ║   │
│   ║   Lv.14  ████████████████████████░  3,765 / 5,000 XP   ║   │
│   ║                                                          ║   │
│   ║   [▶ Next Mission]  [📊 View Debrief]  [🔁 Replay]      ║   │
│   ╚══════════════════════════════════════════════════════════╝   │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### 6.3 Post-Mission Debrief Screen

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  MISSION DEBRIEF: "Pod Can't Talk to Service"                              [Close ✕]   │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│  WHAT HAPPENED                                                                         │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  The `deny-all` NetworkPolicy was applying to ALL pods with an empty podSelector,     │
│  blocking ALL ingress and egress traffic by default.                                   │
│                                                                                        │
│  YOUR FIX                                                                              │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  You added an ingress rule to allow traffic from pods with label `app: frontend`      │
│  to reach pods with label `app: backend` on port 8080.                                │
│                                                                                        │
│  KEY CONCEPTS COVERED                                                                  │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  ● NetworkPolicy default-deny behavior                                                 │
│  ● podSelector vs namespaceSelector                                                    │
│  ● Ingress vs Egress rules                                                             │
│  ● How kube-proxy enforces policy via iptables                                         │
│                                                                                        │
│  YOUR PERFORMANCE VS PEERS                                                             │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  Avg completion time: 28m   |   Your time: 22m ✅ Faster                              │
│  Avg hints used: 1.4        |   Your hints: 0   ✅ None used                          │
│  Avg score: 78%             |   Your score: 94% ✅ Above average                      │
│                                                                                        │
│  RECOMMENDED NEXT                                                                      │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  ┌────────────────────────────┐   ┌────────────────────────────┐                      │
│  │ M3.7: Endpoints vs         │   │ M3.9: Defend the Namespace │                      │
│  │ EndpointSlices             │   │ from East-West Attack      │                      │
│  │ ⚡ 280 XP  ·  ~20 min      │   │ ⚡ 380 XP  ·  ~35 min      │                      │
│  │ [▶ Start]                  │   │ [▶ Start]                  │                      │
│  └────────────────────────────┘   └────────────────────────────┘                      │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 7. X-Ray Mode Overlay

### 7.1 X-Ray Mode Selector

```
┌──────────────────────────────────────────────────────────────────┐
│  [X-Ray Mode Panel — drops down from toolbar]                    │
│                                                                  │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌────────┐ │
│  │  🌐 Network  │ │  💾 Storage  │ │  ⚙ Control  │ │ 🛡 Sec │ │
│  │  X-Ray       │ │  X-Ray       │ │  Plane X-Ray │ │ X-Ray  │ │
│  │  [ACTIVE]    │ │              │ │              │ │        │ │
│  └──────────────┘ └──────────────┘ └──────────────┘ └────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

### 7.2 Network X-Ray Wireframe

```
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  [3D scene with Network X-Ray OVERLAY ACTIVE]                                                    │
│  [Everything slightly dimmed, glow effects on network paths]                                     │
│                                                                                                  │
│    LEGEND: ●─── Allowed  ●─── Blocked  ●─── Pending  ●─── TLS                                  │
│                 (green)        (red)       (amber)   (purple)                                   │
│                                                                                                  │
│    [EXTERNAL CLIENT]                                                                             │
│          │                                                                                       │
│          │  ═══════════════════════════════════════════════════ (animated arrow particles)       │
│          ▼                                                                                       │
│    [GATEWAY OBJECT — glowing orange]                                                             │
│          │ ──────── HTTPRoute evaluation (rule match glow) ──────                               │
│          ▼                                                                                       │
│    [backend-svc — ClusterIP label glowing]                                                       │
│         / \                                                                                      │
│        /   \  (load balancing split — animated)                                                 │
│       ▼     ▼                                                                                    │
│   [back-1]  [back-2]                                                                             │
│   🟢 ALLOWED  🟢 ALLOWED                                                                         │
│                                                                                                  │
│   [between frontend pods and backend pods: RED dashed line = BLOCKED]                           │
│   🔴 frontend-1 ─ ─ ─ ─ ─ ─ ─ ─ X ─ ─ ─ ─ ─ ─ ─ ─ backend-svc                                │
│                                                                                                  │
│   ┌────────────────────────────────────────────────────────────┐                                │
│   │  HOVER INSPECTOR (appears on hover of any flow line)       │                                │
│   │  ─────────────────────────────────────────────────────     │                                │
│   │  Source: frontend-pod-1 (10.244.1.5:52341)                 │                                │
│   │  Destination: backend-svc (10.96.0.100:8080)               │                                │
│   │  Protocol: TCP                                             │                                │
│   │  Status: 🔴 BLOCKED by NetworkPolicy/deny-all              │                                │
│   │  Rule matched: deny-all (empty podSelector + Ingress: [])  │                                │
│   │  [Click to freeze and inspect]                             │                                │
│   └────────────────────────────────────────────────────────────┘                                │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### 7.3 Storage X-Ray Wireframe

```
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  STORAGE X-RAY ACTIVE                                                                            │
│                                                                                                  │
│    ┌──────────────────────────────────────────────────────────────────────────────────────────┐ │
│    │ STORAGE TOPOLOGY                                                                         │ │
│    │                                                                                          │ │
│    │  [StorageClass]                                                                          │ │
│    │  standard-ssd                                                                            │ │
│    │  provisioner: kubernetes.io/gce-pd                                                       │ │
│    │       │                                                                                  │ │
│    │       │  (dynamic provisioning arrow — animated downward)                               │ │
│    │       ▼                                                                                  │ │
│    │  [PV: pv-database-01]   ◄──────────────── [PVC: db-data]                                │ │
│    │  💾 10Gi, ReadWriteOnce   BOUND ●─────────────── BOUND ●                                │ │
│    │       │                                                                                  │ │
│    │       │  (mount path animation — glowing line going UP to pod)                          │ │
│    │       ▼                                                                                  │ │
│    │  [Pod: postgres-0]                                                                       │ │
│    │  🟢 Running                                                                              │ │
│    │  Volume mounted at: /var/lib/postgresql/data                                             │ │
│    │  I/O Activity: ████░░░░  (real-time read/write indicator)                               │ │
│    │                                                                                          │ │
│    │  [Hover: PV details panel]                                                               │ │
│    │  ┌────────────────────────────────────────────┐                                         │ │
│    │  │  PV: pv-database-01                        │                                         │ │
│    │  │  Capacity: 10Gi                             │                                         │ │
│    │  │  Access Mode: ReadWriteOnce                 │                                         │ │
│    │  │  Reclaim Policy: Retain                     │                                         │ │
│    │  │  Status: Bound                              │                                         │ │
│    │  │  Claim: default/db-data                     │                                         │ │
│    │  └────────────────────────────────────────────┘                                         │ │
│    └──────────────────────────────────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 8. XP System Design

### 8.1 XP Progress Bar Component (Header)

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│  [Lv.14 Navigator]   ⚡ 3,765 / 5,000 XP   [1,235 to Lv.15] │
│  ████████████████████████████████░░░░░░░░░░░░  75.3%        │
│                                                              │
│  [Pulsing glow on the filled portion]                        │
│  [XP gain: animated counter +525 floating up when earned]    │
└──────────────────────────────────────────────────────────────┘
```

### 8.2 Level Milestone Screen

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   [Full-screen takeover — dark with particle burst]              │
│                                                                  │
│   ╔══════════════════════════════════════════════════════════╗   │
│   ║                                                          ║   │
│   ║         ⚡  LEVEL UP!  ⚡                                ║   │
│   ║                                                          ║   │
│   ║         [Animated badge morphing from 14 → 15]           ║   │
│   ║                                                          ║   │
│   ║   You are now:                                           ║   │
│   ║   ─────────────────────────────────────────────         ║   │
│   ║   Level 15  |  Navigator  [Blue badge]                  ║   │
│   ║                                                          ║   │
│   ║   UNLOCKED:                                              ║   │
│   ║   🧪 Sandbox Mode — Build freely without missions       ║   │
│   ║   🌍 Community Missions — Share & explore user content  ║   │
│   ║                                                          ║   │
│   ║   NEXT MILESTONE                                         ║   │
│   ║   Level 21 → Engineer  [Purple badge]                   ║   │
│   ║   Unlocks: Chaos Lab                                     ║   │
│   ║                                                          ║   │
│   ║   [Continue ▶]                                           ║   │
│   ╚══════════════════════════════════════════════════════════╝   │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### 8.3 XP Ledger / History Panel

```
┌────────────────────────────────────────────────────────────────────────────┐
│  MY XP HISTORY                                                 [Filter ▼]  │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Today                                                                     │
│  ─────────────────────────────────────────────────────────────────────     │
│  ⚡ +525   Mission 3.6: Pod Can't Talk to Service          14:52 today    │
│  ⚡ +50    Achievement: "Policy Enforcer"                  14:52 today    │
│  ⚡ +200   7-Day Streak Bonus                              08:00 today    │
│                                                                            │
│  Yesterday                                                                 │
│  ─────────────────────────────────────────────────────────────────────     │
│  ⚡ +300   Mission 3.5: NetworkPolicy: Namespace Isolation  20:14 yest.   │
│  ⚡ +250   Mission 3.4: DNS Resolution: CoreDNS in Action  18:30 yest.   │
│  ⚡ +25    Daily Challenge: "The Broken Service"           09:00 yest.   │
│  ⚡ -20    Hint used (Tier 2)                              18:45 yest.   │
│                                                                            │
│  TOTALS THIS WEEK:  ⚡ 3,240 XP                                           │
│  ████████████░░░░░░░░░░░░░░░░░░░░  vs last week: +48%                     │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

### 8.4 Skill Tree Screen

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  SKILL TREE                            [Zoom: -  100%  +]   [Reset View]               │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│   [Panning / zooming 2D skill tree view with glow connections between nodes]          │
│                                                                                        │
│                              ┌─────────────────────┐                                  │
│                              │  CORE OPERATIONS    │                                  │
│                              │  ████████████  LV4  │  ← UNLOCKED (cyan glow)         │
│                              └──────────┬──────────┘                                  │
│                                         │                                              │
│               ┌─────────────────────────┼──────────────────────┐                      │
│               │                         │                      │                      │
│    ┌──────────▼──────────┐   ┌──────────▼──────────┐  ┌───────▼───────────────┐      │
│    │   NETWORKING        │   │   STORAGE            │  │  SECURITY             │      │
│    │   ██████████  LV3   │   │   ████░░░░  LV2      │  │  ██░░░░░░  LV1        │      │
│    └──────────┬──────────┘   └──────────┬──────────┘  └───────┬───────────────┘      │
│               │                         │                      │                      │
│    ┌──────────▼──────────┐   ┌──────────▼──────────┐  ┌───────▼───────────────┐      │
│    │  GATEWAY API        │   │  DATA SERVICES      │  │  POLICY ENGINE        │      │
│    │  ██░░░░░░  LV1      │   │  🔒 LOCKED          │  │  🔒 LOCKED            │      │
│    └──────────┬──────────┘   └─────────────────────┘  └───────────────────────┘      │
│               │                                                                        │
│    ┌──────────▼──────────┐                                                            │
│    │  kgateway           │                                                            │
│    │  🔒 LOCKED          │                                                            │
│    └─────────────────────┘                                                            │
│                                                                                        │
│   [Click any node → side panel shows: missions required, XP needed, what it unlocks]  │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 9. Achievement Screen

### 9.1 Achievement Gallery

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  ACHIEVEMENTS                                                                          │
│  23 earned · 127 remaining · 20 secret                                                │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│  [Filter by Category]                                                                  │
│  [All] [First Steps] [Speed Demon] [Chaos Master] [Gateway Guru] [Secret] [Earned]    │
│                                                                                        │
│  RECENTLY EARNED                                                                       │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│                                                                                        │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐                    │
│  │  [Gold badge]    │  │  [Silver badge]  │  │  [Bronze badge]  │                    │
│  │  🛡 Policy       │  │  🚫 No-Hinter    │  │  🌐 DNS Wizard   │                    │
│  │  Enforcer        │  │                  │  │                  │                    │
│  │                  │  │  Complete 5      │  │  Resolve DNS     │                    │
│  │  Fix your first  │  │  missions with   │  │  query 10 times  │                    │
│  │  NetworkPolicy   │  │  no hints        │  │                  │                    │
│  │                  │  │                  │  │                  │                    │
│  │  ⚡ +100 XP      │  │  ⚡ +300 XP      │  │  ⚡ +75 XP       │                    │
│  │  2h ago  [Share] │  │  1d ago  [Share] │  │  2d ago  [Share] │                    │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘                    │
│                                                                                        │
│  ALL ACHIEVEMENTS — FIRST STEPS (8/10)                                                │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│                                                                                        │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐                    │
│  │ ✅ [Badge]       │  │ ✅ [Badge]       │  │ 🔒 [Locked]      │                    │
│  │  Hello K8s       │  │  Pod Whisperer   │  │  The Scheduler   │                    │
│  │  Earned 3w ago   │  │  Earned 1w ago   │  │  Schedule a Pod  │                    │
│  │                  │  │                  │  │  manually        │                    │
│  │  COMMON          │  │  RARE            │  │  RARE            │                    │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘                    │
│                                                                                        │
│  SECRET ACHIEVEMENTS (? / 20)                                                          │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│                                                                                        │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐                    │
│  │  [? silhouette] │  │  [? silhouette] │  │  [? silhouette] │                    │
│  │  ???             │  │  ???             │  │  ???             │                    │
│  │  Hidden          │  │  Hidden          │  │  Hidden          │                    │
│  │  achievement     │  │  achievement     │  │  achievement     │                    │
│  │  LEGENDARY       │  │  EPIC            │  │  RARE            │                    │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘                    │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

### 9.2 Achievement Unlock Animation (Overlay)

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   [Slides in from bottom-right — toast style]                   │
│                                                                  │
│   ╔══════════════════════════════════════════════════╗          │
│   ║  🏆 ACHIEVEMENT UNLOCKED                         ║          │
│   ║                                                  ║          │
│   ║  [Badge spins in]  Policy Enforcer              ║          │
│   ║  Fix your first NetworkPolicy                   ║          │
│   ║  ⚡ +100 XP  ·  COMMON                          ║          │
│   ║                                                  ║          │
│   ║  [Share on LinkedIn]  [Share on Twitter]         ║          │
│   ╚══════════════════════════════════════════════════╝          │
│   [Auto-dismisses after 6 seconds]                              │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### 9.3 Shareable Achievement Card

```
┌────────────────────────────────────────────────────────────────┐
│                                                                │
│  [Generated as PNG for sharing]                               │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │  [CloudQuest AI logo]           [Starfield background]   │ │
│  │                                                          │ │
│  │          [LARGE BADGE GRAPHIC — glowing, 3D-ish]         │ │
│  │                                                          │ │
│  │                Policy Enforcer                           │ │
│  │          "Fix your first NetworkPolicy"                  │ │
│  │                                                          │ │
│  │    Kai Ramirez  ·  Level 14 Navigator  ·  ⚡ +100 XP     │ │
│  │                                                          │ │
│  │    cloudquest.ai  ·  #CloudQuestAI  ·  #Kubernetes       │ │
│  └──────────────────────────────────────────────────────────┘ │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

---

## 10. User Profile Screen

### 10.1 Public Profile

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  PROFILE                                                       [Edit Profile ✏]        │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐ │
│  │  [Profile Banner — animated cluster background, customizable skin]               │ │
│  │                                                                                  │ │
│  │  [Avatar 96px]  Kai Ramirez                                                      │ │
│  │                 @kai_ramirez                                                      │ │
│  │                 ⚡ Level 14  ·  Navigator  [Blue Badge]                          │ │
│  │                 🔥 7-day streak  ·  Member since Jan 2026                         │ │
│  │                 📍 Manila, Philippines                                            │ │
│  └──────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                        │
│  STATS OVERVIEW                                                                        │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐          │
│  │  Total XP │  │ Missions  │  │ Badges    │  │ Global    │  │ Streak    │          │
│  │  21,450   │  │  47 done  │  │  23       │  │ #1,204    │  │  7 days   │          │
│  └───────────┘  └───────────┘  └───────────┘  └───────────┘  └───────────┘          │
│                                                                                        │
│  ┌──────────────────────────────────────────┐  ┌──────────────────────────────────┐  │
│  │  SKILL PROFILE                           │  │  TOP ACHIEVEMENTS                │  │
│  │  ────────────────────────────────────    │  │  ────────────────────────────    │  │
│  │                                          │  │                                  │  │
│  │  Networking    ████████████████  Lv.3    │  │  [Badge] Policy Enforcer         │  │
│  │  Storage       █████████░░░░░░░  Lv.2    │  │  [Badge] No-Hinter               │  │
│  │  Security      ████░░░░░░░░░░░░  Lv.1    │  │  [Badge] DNS Wizard              │  │
│  │  Gateway API   ██░░░░░░░░░░░░░░  Lv.1    │  │  [Badge] Hello Kubernetes        │  │
│  │  Operations    ██████████░░░░░░  Lv.2    │  │  [Badge] Pod Whisperer           │  │
│  │                                          │  │                                  │  │
│  │  [View Full Skill Tree →]                │  │  [View All 23 Achievements →]    │  │
│  └──────────────────────────────────────────┘  └──────────────────────────────────┘  │
│                                                                                        │
│  LEARNING PROGRESS                                                                     │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  Module 1: Cluster Genesis        18/18  ████████████████████  100% ✅               │
│  Module 2: Workloads              22/22  ████████████████████  100% ✅               │
│  Module 3: Networking              5/25  ████░░░░░░░░░░░░░░░░   20% 🔵              │
│  Module 4–10                      Locked                                              │
│                                                                                        │
│  RECENT ACTIVITY                                                                       │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  ✅ Completed M3.6: Pod Can't Talk to Service         2h ago    Score: 94%  ⚡+525   │
│  🏆 Earned: Policy Enforcer                           2h ago                          │
│  ✅ Completed M3.5: NetworkPolicy: Namespace Isolation 1d ago   Score: 88%  ⚡+300   │
│                                                                                        │
│  REPLAYS & SHARED CONTENT                                                              │
│  ─────────────────────────────────────────────────────────────────────────────────    │
│  ┌──────────────────────┐  ┌──────────────────────┐                                  │
│  │  [Replay thumbnail]  │  │  [Replay thumbnail]  │                                  │
│  │  M3.6 Speedrun       │  │  M2.8 CrashLoop Fix  │                                  │
│  │  👁 142 views · ❤ 28 │  │  👁 89 views · ❤ 15  │                                  │
│  └──────────────────────┘  └──────────────────────┘                                  │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 11. AI Mentor Interface

### 11.1 AI Mentor Sidebar (in Simulator)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│  [3D Simulator — main view takes 65% of width]   [AI MENTOR — 35% right panel] │
├──────────────────────────────────────────────────┬──────────────────────────────┤
│                                                  │                              │
│  [3D cluster scene]                              │  🤖 AI MENTOR               │
│                                                  │  ARIA — CloudQuest Guide    │
│                                                  │                              │
│                                                  │  ┌──────────────────────┐   │
│                                                  │  │ [Animated AI Avatar  │   │
│                                                  │  │  — holographic style,│   │
│                                                  │  │  pulsing ring around │   │
│                                                  │  │  it when speaking]   │   │
│                                                  │  └──────────────────────┘   │
│                                                  │                              │
│                                                  │  MISSION CONTEXT             │
│                                                  │  M3.6 · Progress: 0/4 obj   │
│                                                  │                              │
│                                                  │  ──────────────────────────  │
│                                                  │  ARIA:                       │
│                                                  │                              │
│                                                  │  I see you've opened the    │
│                                                  │  NetworkPolicy YAML. Before  │
│                                                  │  you edit it — what does an │
│                                                  │  empty `podSelector: {}`     │
│                                                  │  actually select?            │
│                                                  │                              │
│                                                  │  [🔊 Voice mode ON]          │
│                                                  │                              │
│                                                  │  ──────────────────────────  │
│                                                  │  YOU:                        │
│                                                  │  I think it selects all     │
│                                                  │  pods?                       │
│                                                  │                              │
│                                                  │  ──────────────────────────  │
│                                                  │  ARIA:                       │
│                                                  │                              │
│                                                  │  Exactly right! So if the   │
│                                                  │  policy selects ALL pods,   │
│                                                  │  and has empty ingress      │
│                                                  │  rules... what happens to   │
│                                                  │  ALL traffic into those     │
│                                                  │  pods?                       │
│                                                  │                              │
│                                                  │  [💡 Callout: highlighted   │
│                                                  │  NetworkPolicy in 3D scene] │
│                                                  │                              │
│                                                  │  ──────────────────────────  │
│                                                  │                              │
│                                                  │  HINTS AVAILABLE: 3         │
│                                                  │  [💡 Use Hint — costs 10 XP]│
│                                                  │                              │
│                                                  │  ──────────────────────────  │
│                                                  │  [Type your response...]    │
│                                                  │  [Send ▶]                   │
│                                                  │                              │
│                                                  │  [Mode: Guide ▼]            │
│                                                  │  ○ Guide  ○ Explain  ○ Quiz │
│                                                  │                              │
└──────────────────────────────────────────────────┴──────────────────────────────┘
```

### 11.2 AI Mentor Hint Tier Panel

```
┌────────────────────────────────────────────────────────────────────────────────┐
│  USE A HINT?                                                        [Close ✕]  │
├────────────────────────────────────────────────────────────────────────────────┤
│                                                                                │
│  ┌──────────────────────────────────────────────────────────────────────────┐ │
│  │  HINT TIER 1 — Conceptual Nudge                         Cost: -10 XP    │ │
│  │  ──────────────────────────────────────────────────────────────────────  │ │
│  │  "Think about what happens when a NetworkPolicy has ingress rules        │ │
│  │  defined as an empty list vs having no ingress field at all."            │ │
│  │                                                                          │ │
│  │  [Reveal Hint 1]                                                         │ │
│  └──────────────────────────────────────────────────────────────────────────┘ │
│                                                                                │
│  ┌──────────────────────────────────────────────────────────────────────────┐ │
│  │  HINT TIER 2 — Visual Callout                           Cost: -20 XP    │ │
│  │  ──────────────────────────────────────────────────────────────────────  │ │
│  │  [Locked until Tier 1 used]                                              │ │
│  │  Highlights the exact field in the YAML and the pod in the 3D scene.    │ │
│  └──────────────────────────────────────────────────────────────────────────┘ │
│                                                                                │
│  ┌──────────────────────────────────────────────────────────────────────────┐ │
│  │  HINT TIER 3 — Near Answer                             Cost: -40 XP    │ │
│  │  ──────────────────────────────────────────────────────────────────────  │ │
│  │  [Locked until Tier 2 used]                                              │ │
│  │  Near-direct guidance with the exact YAML structure to add.              │ │
│  └──────────────────────────────────────────────────────────────────────────┘ │
│                                                                                │
│  ⚠ Using hints reduces your XP for this mission.                             │
│  Your current XP balance: ⚡ 3,765                                            │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

### 11.3 AI Mentor — Explain Mode (Full Screen)

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│  ARIA EXPLAINS: NetworkPolicy — How Ingress Rules Work                    [✕ Close]   │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│  ┌────────────────────────────────────────┐  ┌──────────────────────────────────────┐ │
│  │  [3D Cluster — controlled view]        │  │  ARIA'S EXPLANATION                  │ │
│  │  [Showing pods + policy with           │  │  ────────────────────────────────    │ │
│  │   animated callouts synced to text]    │  │                                      │ │
│  │                                        │  │  A NetworkPolicy with:               │ │
│  │  [Arrow 1: points to podSelector]      │  │                                      │ │
│  │  [Arrow 2: points to ingress: []]      │  │  `podSelector: {}`                   │ │
│  │  [Animation: traffic blocked]          │  │  selects ALL pods in the namespace.  │ │
│  │                                        │  │                          ↑           │ │
│  │                                        │  │                    [Callout 1 →]     │ │
│  │                                        │  │                                      │ │
│  │                                        │  │  `ingress: []`                       │ │
│  │                                        │  │  is an EMPTY list — meaning NO       │ │
│  │                                        │  │  ingress rules = DENY ALL inbound.  │ │
│  │                                        │  │                          ↑           │ │
│  │                                        │  │                    [Callout 2 →]     │ │
│  │                                        │  │                                      │ │
│  │                                        │  │  To allow frontend → backend:        │ │
│  │                                        │  │  Add an ingress rule that            │ │
│  │                                        │  │  specifies the source pod label.     │ │
│  │                                        │  │                                      │ │
│  │                                        │  │  [▶ Next concept]  [✓ Got it]        │ │
│  └────────────────────────────────────────┘  └──────────────────────────────────────┘ │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 12. Mobile Responsive Layout

### 12.1 Mobile Dashboard (375px — iPhone)

```
┌───────────────────────────┐
│  ☰  CloudQuest AI    [🔔] │   ← Top bar (hamburger + notification)
├───────────────────────────┤
│                           │
│  👋 Good evening, Kai     │
│  Lv.14 · Navigator        │
│  ⚡ 3,765 / 5,000 XP      │
│  █████████████░░░  75%    │
│                           │
│  [▶ Resume Mission]       │
│  M3.6 · ~12 min left      │
│                           │
├───────────────────────────┤
│  TODAY'S STATS            │
│  ┌────────┐  ┌────────┐   │
│  │ 🎯 47  │  │ 🔥 7d  │   │
│  │missions│  │ streak │   │
│  └────────┘  └────────┘   │
│  ┌────────┐  ┌────────┐   │
│  │ 🏆 23  │  │ #1,204 │   │
│  │ badges │  │ global │   │
│  └────────┘  └────────┘   │
│                           │
├───────────────────────────┤
│  CONTINUE LEARNING        │
│  ──────────────────────   │
│  ┌───────────────────────┐│
│  │ 🔵 M3.6 · FIX-IT      ││
│  │ Pod Can't Talk to Svc ││
│  │ ⚡ 300 XP · ~30 min   ││
│  │ [▶ Resume]            ││
│  └───────────────────────┘│
│  ┌───────────────────────┐│
│  │ ⬜ M3.7 · BUILD-IT    ││
│  │ Endpoints vs Slices   ││
│  │ ⚡ 280 XP · ~20 min   ││
│  │ [▶ Start]             ││
│  └───────────────────────┘│
│                           │
├───────────────────────────┤
│  DAILY CHALLENGE  🏁      │
│  "Fix the Broken Service" │
│  ⏱ ~15 min  ·  ⚡ 250 XP  │
│  [▶ Start Challenge]      │
│                           │
└───────────────────────────┘
│  [🏠] [🗺] [🎮] [🏆] [👤] │   ← Bottom tab bar
└───────────────────────────┘
```

### 12.2 Mobile Mission Select (375px)

```
┌───────────────────────────┐
│  ← Modules   Networking   │
├───────────────────────────┤
│                           │
│  Module 3: Networking     │
│  5/25  ·  ⚡ 850 XP       │
│  ████░░░░░░░░░░░  20%     │
│                           │
│  Filter: [All ▼]          │
│                           │
│  ┌───────────────────────┐│
│  │ ✅ 3.1 · Investigate  ││
│  │ ClusterIP: How it     ││
│  │ Works                 ││
│  │ ⚡ 150 XP  Score: 94% ││
│  │ [Replay]              ││
│  └───────────────────────┘│
│  ┌───────────────────────┐│
│  │ 🔵 3.5 · Build-It     ││
│  │ NetworkPolicy         ││
│  │ ⚡ 280 XP  In Progress ││
│  │ [▶ Resume]            ││
│  └───────────────────────┘│
│  ┌───────────────────────┐│
│  │ ⬜ 3.6 · Fix-It       ││
│  │ Pod Can't Talk to Svc ││
│  │ ⚡ 300 XP  ~30 min    ││
│  │ [▶ Start]             ││
│  └───────────────────────┘│
│  ┌───────────────────────┐│
│  │ 🔒 3.10 · X-Ray       ││
│  │ Trace Request to Pod  ││
│  │ Requires: 3.9         ││
│  └───────────────────────┘│
└───────────────────────────┘
```

### 12.3 Mobile 3D Simulator (375px — Landscape)

```
┌──────────────────────────────────────────────────────────────────┐
│  [← Exit]  M3.6  ·  ⏱ 12:34  ·  ⚡ 300 XP  ·  [🤖]  [X-Ray]   │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  [3D VIEWPORT — full width, 55% of height]                      │
│                                                                  │
│  [Simplified cluster view: 2 nodes, pods as dots, service lines]│
│                                                                  │
│  [Pinch to zoom  ·  drag to orbit]                              │
│                                                                  │
├──────────────────────────────────────────────────────────────────┤
│  Objectives [1⬜][2⬜][3⬜][4⬜]    [Inspector ▲] [YAML ▲]       │
├──────────────────────────────────────────────────────────────────┤
│  EVENTS LOG (scrollable)                                         │
│  ⚠ NetworkPolicy/deny-all applied...                            │
│  ✗ frontend-1 → backend-svc: Connection refused                  │
│  [Show more...]                                                  │
│                                                                  │
│  [🤖 Ask ARIA]          [💡 Hint (3 left)]                      │
└──────────────────────────────────────────────────────────────────┘
```

### 12.4 Mobile AI Mentor (375px — Full Screen)

```
┌───────────────────────────┐
│  ← Back    🤖 ARIA        │
├───────────────────────────┤
│                           │
│  [Animated avatar — top   │
│   center of screen]       │
│                           │
│  ──────────────────────   │
│  ARIA                     │
│                           │
│  What does an empty       │
│  `podSelector: {}` select │
│  in Kubernetes?           │
│                           │
│  [Highlight Object 🔍]    │
│                           │
│  ──────────────────────   │
│  YOU                      │
│                           │
│  All pods in namespace?   │
│                           │
│  ──────────────────────   │
│  ARIA                     │
│                           │
│  Correct! So with empty   │
│  ingress rules what       │
│  happens to traffic?      │
│                           │
│                           │
│                           │
│                           │
│                           │
│                           │
│                           │
├───────────────────────────┤
│  [Type here...]   [Send ▶]│
│  [💡 Hint -10 XP]         │
└───────────────────────────┘
```

### 12.5 Mobile Achievements (375px)

```
┌───────────────────────────┐
│  ← Back    ACHIEVEMENTS   │
├───────────────────────────┤
│  23 earned · 127 remaining│
│                           │
│  [All][First Steps][Speed]│
│  [Chaos][Gateway][Secret] │
│                           │
│  RECENTLY EARNED          │
│  ──────────────────────   │
│  ┌───────────────────────┐│
│  │ [Badge] Policy Enforcer││
│  │ Fix your first        ││
│  │ NetworkPolicy         ││
│  │ ⚡ +100  COMMON  2h ago││
│  │                [Share]││
│  └───────────────────────┘│
│  ┌───────────────────────┐│
│  │ [Badge] No-Hinter     ││
│  │ 5 missions, no hints  ││
│  │ ⚡ +300  RARE   1d ago ││
│  │                [Share]││
│  └───────────────────────┘│
│                           │
│  ALL — FIRST STEPS (8/10) │
│  ──────────────────────   │
│  ┌──────┐┌──────┐┌──────┐ │
│  │ ✅   ││ ✅   ││ 🔒   │ │
│  │Hello ││Pod   ││Sched-│ │
│  │K8s   ││Whisp.││uler  │ │
│  └──────┘└──────┘└──────┘ │
└───────────────────────────┘
│  [🏠] [🗺] [🎮] [🏆] [👤] │
└───────────────────────────┘
```

### 12.6 Responsive Breakpoint System

| Breakpoint | Width | Layout Changes |
|---|---|---|
| Mobile S | 320px | Single column, bottom nav, simplified 3D |
| Mobile L | 375–428px | Single column, bottom nav, full 3D landscape |
| Tablet | 768px | 2-column layout, sidebar drawer, full 3D |
| Laptop | 1024px | Left sidebar (collapsed), full 3D viewport |
| Desktop | 1280px+ | Left sidebar (expanded), full 3D + side panels |
| Wide | 1440px+ | Full layout as designed (optimal experience) |

### 12.7 Mobile-Specific UX Rules

| Rule | Rationale |
|---|---|
| Bottom tab bar (5 items max) | Thumb-reachable primary navigation |
| 3D scene: pinch-zoom + drag-orbit | Touch-native 3D interaction |
| Simplified 3D on mobile (fewer objects) | Performance on mobile GPU |
| YAML editor: full-screen mode | Keyboard doesn't obscure content |
| AI Mentor: full-screen modal on mobile | Reading space for conversations |
| Achievements: card list (not grid) | Single-column is more scannable |
| Mission complete overlay: centered modal | Legible on small screen |
| Streak / XP always visible in top bar | Constant motivational reinforcement |

---

## Design Summary

### Screen Inventory

| Screen | Desktop Layout | Mobile Layout | Key Interactions |
|---|---|---|---|
| Dashboard | 2-col + stats | Single-col + bottom nav | Resume, Daily Challenge |
| Module Overview | 3-col card grid | Vertical list | Filter, lock states |
| Mission Briefing | 2-col split | Single-col scroll | Launch, read objectives |
| 3D Simulator | Full-screen + right panel | Landscape + bottom panels | Orbit, click, inspect |
| X-Ray Mode | Overlay on 3D | Overlay on 3D | Toggle, hover, freeze |
| Mission Complete | Centered overlay | Centered modal | Share, next mission |
| Debrief | Full-page | Scrollable page | Concepts, replay |
| XP / Level Up | Full-screen takeover | Full-screen takeover | Continue |
| Skill Tree | Pannable 2D canvas | Scrollable list | Click nodes |
| Achievements | 3-col masonry | List + 3-col mini | Filter, share |
| Profile | Header + 2-col | Single-col scroll | Edit, view history |
| AI Mentor | Right sidebar panel | Full-screen modal | Chat, hints, modes |
| Leaderboard | Table with ranks | List with ranks | Filter, period |

---

*UI/UX Design Document — Version 1.0 | CloudQuest AI | June 2026*
*Principal Product Architect*
