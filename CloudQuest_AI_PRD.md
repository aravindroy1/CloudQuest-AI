# CloudQuest AI — Product Requirements Document
### Version 1.0 | Principal Product Architect Edition | June 2026

---

> **Vision Statement**  
> CloudQuest AI is not a course. It is not a tutorial. It is a living, breathing Kubernetes universe — a 3D interactive simulator where every concept becomes a visual, tactile experience. Users don't just learn Kubernetes; they *inhabit* it.

---

## Table of Contents

1. [Product Requirements Document (PRD)](#1-product-requirements-document)
2. [User Personas](#2-user-personas)
3. [Feature List](#3-feature-list)
4. [Module Breakdown](#4-module-breakdown)
5. [User Flows](#5-user-flows)
6. [Learning Path](#6-learning-path)
7. [Gamification System](#7-gamification-system)
8. [Database Design](#8-database-design)
9. [Technical Architecture](#9-technical-architecture)
10. [Development Roadmap](#10-development-roadmap)

---

## 1. Product Requirements Document

### 1.1 Executive Summary

**Product Name:** CloudQuest AI  
**Product Type:** 3D Interactive Kubernetes Simulation Platform  
**Target Market:** Students, Freshers, Junior DevOps Engineers, Cloud Engineers  
**Business Model:** Freemium + Enterprise Licensing  
**Platform:** Web (primary), Desktop Electron app (secondary)

CloudQuest AI transforms Kubernetes education by replacing static documentation and video tutorials with an immersive 3D simulator. Every Kubernetes primitive — Pod, Node, Deployment, Service, Ingress, PersistentVolume, Gateway API, NetworkPolicy — is rendered as an interactive 3D object inside a living cluster environment. Users perform real operations, trigger real failures, and watch the system respond in real time.

---

### 1.2 Problem Statement

| Pain Point | Current State | CloudQuest AI Solution |
|---|---|---|
| Kubernetes is abstract | Concepts exist only in YAML/text | Every concept is a visible 3D object |
| Labs feel disconnected | Click-through tutorials with no narrative | Mission-based stories with stakes |
| No failure practice | Users only practice happy paths | Failure Simulation Engine with chaos injection |
| No feedback loop | Users don't know if they understood | AI Mentor provides real-time Socratic guidance |
| Gateway API is opaque | Hard to visualize routing rules | Interactive traffic flow visualization |
| Storage is mysterious | PV/PVC lifecycle not visible | Live storage binding animations |
| Networking is invisible | CIDR, CNI, NetworkPolicy — all text | X-Ray Mode shows live packet paths |

---

### 1.3 Product Goals

**Primary Goals:**
- Reduce average Kubernetes learning time from 6 months to 6 weeks
- Achieve 70%+ mission completion rate (industry benchmark: 30%)
- Become the #1 Kubernetes simulator by Q4 2027

**Secondary Goals:**
- Generate enterprise revenue via team licenses and custom mission packs
- Build an open mission ecosystem via community SDK
- Partner with CNCF for certification prep content

---

### 1.4 Success Metrics (KPIs)

| Metric | Target (6 months) | Target (12 months) |
|---|---|---|
| Monthly Active Users (MAU) | 50,000 | 250,000 |
| Mission Completion Rate | ≥ 65% | ≥ 75% |
| Day-7 Retention | ≥ 40% | ≥ 55% |
| Day-30 Retention | ≥ 20% | ≥ 35% |
| NPS Score | ≥ 60 | ≥ 75 |
| Avg. Session Duration | ≥ 25 min | ≥ 35 min |
| XP Earned per User/Week | ≥ 500 XP | ≥ 1,200 XP |
| AI Mentor Engagement Rate | ≥ 50% | ≥ 70% |

---

### 1.5 Constraints & Assumptions

**Constraints:**
- Must run on mid-tier hardware (no GPU required for core experience)
- Browser-first — no native install required for basic tier
- All simulations must be deterministic and reproducible
- GDPR compliant from day 1

**Assumptions:**
- Users have basic Linux CLI familiarity
- Users have at minimum heard of containers/Docker
- Enterprise teams use existing IDP (SAML/OIDC)

---

### 1.6 Out of Scope (v1.0)

- Real cluster provisioning (EKS, GKE, AKS integration) — Phase 2
- Mobile app — Phase 3
- Custom CNI plugin simulations — Phase 2
- Multi-tenant enterprise cluster management — Phase 3

---

## 2. User Personas

---

### Persona 1: Kai — The Curious CS Student

```
Name:        Kai Ramirez
Age:         21
Role:        Final-year Computer Science Student
Location:    Manila, Philippines
Device:      Mid-range laptop, 8GB RAM
Goal:        Land a cloud internship before graduation
Frustration: "I read the Kubernetes docs but nothing sticks"
```

**Behavioral Profile:**
- Learns by doing, not reading
- Highly competitive — loves leaderboards
- Shares achievements on LinkedIn and Discord
- Studies in 30–60 minute bursts
- Motivated by visible progress and badges

**CloudQuest AI Usage Pattern:**
- Completes 2–3 missions per week
- Shares achievement cards on social media
- Uses AI Mentor to understand why something failed
- Targets CKA certification track

**Key Jobs-to-be-Done:**
1. Understand Kubernetes well enough to discuss in interviews
2. Get a portfolio-worthy project
3. Beat friends on the leaderboard

---

### Persona 2: Priya — The Career Switcher Fresher

```
Name:        Priya Nair
Age:         24
Role:        Recent BCA Graduate, 0 years experience
Location:    Bengaluru, India
Device:      Windows laptop, 4GB RAM (shared family computer)
Goal:        Get first DevOps role within 6 months
Frustration: "DevOps jobs require experience, but how do I get experience?"
```

**Behavioral Profile:**
- Deeply motivated but lacks confidence
- Needs encouragement and scaffolding
- Learns best with visual metaphors
- Studies 1–2 hours per day consistently
- Anxious about "breaking things"

**CloudQuest AI Usage Pattern:**
- Follows guided learning path strictly
- Uses AI Mentor extensively for clarification
- Replays missions to improve scores
- Prefers structured missions over sandbox

**Key Jobs-to-be-Done:**
1. Build enough knowledge to pass first DevOps screening
2. Understand why things work, not just how
3. Practice safely without fear of breaking production

---

### Persona 3: Marcus — The Junior DevOps Engineer

```
Name:        Marcus Chen
Age:         27
Role:        Junior DevOps Engineer (1.5 years exp)
Location:    Austin, TX
Device:      MacBook Pro, 16GB RAM
Goal:        Earn CKA + move into senior role
Frustration: "I can write YAML but I don't really understand what happens inside"
```

**Behavioral Profile:**
- Hands-on, pragmatic, time-constrained
- Already uses kubectl but wants depth
- Interested in networking and storage internals
- Competitive — wants to outperform peers
- Values efficiency over aesthetics

**CloudQuest AI Usage Pattern:**
- Skips beginner content, jumps to intermediate/advanced missions
- Heavy user of X-Ray Mode (networking/storage internals)
- Uses Failure Simulation to practice incident response
- Participates in weekly challenge missions

**Key Jobs-to-be-Done:**
1. Deeply understand Kubernetes internals for CKA
2. Practice troubleshooting and failure recovery
3. Demonstrate expertise to manager/team

---

### Persona 4: Anya — The Cloud Engineer Upskiller

```
Name:        Anya Voronova
Age:         31
Role:        Cloud Engineer (AWS/GCP), 4 years exp
Location:    Berlin, Germany
Device:      ThinkPad X1, corporate managed
Goal:        Add Kubernetes/Gateway API expertise to cloud skills
Frustration: "Gateway API docs are terrible — I need to SEE how routing works"
```

**Behavioral Profile:**
- Expert in cloud primitives, new to K8s internals
- Focused on Gateway API, networking, and storage
- Time-poor — needs focused, high-value sessions
- Prefers sandbox exploration over guided missions
- Values professional certifications

**CloudQuest AI Usage Pattern:**
- Uses sandbox mode extensively
- Focuses on Gateway API and Networking modules
- Uses AI Mentor for deep technical Q&A
- Skips gamification, cares about knowledge

**Key Jobs-to-be-Done:**
1. Understand Gateway API + kgateway deeply
2. Map familiar cloud concepts to Kubernetes equivalents
3. Rapidly build expertise for team leadership

---

## 3. Feature List

### 3.1 Core Features (Must-Have — v1.0)

#### F-001: 3D Cluster Visualization Engine
- Real-time 3D rendering of Kubernetes clusters using Three.js / WebGL
- Nodes rendered as server racks in a data center environment
- Pods rendered as animated containers with health indicators
- Control Plane visible as a separate elevated "command tower"
- Deployments, ReplicaSets, StatefulSets rendered with distinct visual identities
- Camera controls: orbit, zoom, pan, focus-on-object
- Object inspector: click any 3D object to see its spec, status, events

#### F-002: Kubernetes Event Simulation Engine
- Deterministic simulation of all core K8s control loops
- Scheduler simulation: visualize scoring, filtering, binding
- Controller Manager simulation: ReplicaSet reconciliation, Deployment rollout
- etcd state store: visualize reads/writes with animated data flows
- API Server: visualize request processing pipeline
- Kubelet: visualize pod lifecycle on each node
- All operations real-time animated with configurable speed (0.25x → 4x)

#### F-003: Mission-Based Learning System
- 200+ structured missions across 10 modules
- Each mission has: Briefing → Objective → Sandbox → Validation → Debrief
- Mission types: Fix-It, Build-It, Investigate, Race-Against-Time, Defend
- Auto-grading with partial credit
- Mission replay for score improvement
- Mission branching: different paths based on choices made

#### F-004: X-Ray Mode
- Toggle X-Ray overlay on cluster at any time
- **Network X-Ray**: visualize live packet paths between Pods, Services, Gateways
- **Storage X-Ray**: visualize PV/PVC binding, mount paths, I/O operations
- **Control Plane X-Ray**: visualize reconciliation loops, leader election, etcd
- **Security X-Ray**: visualize RBAC evaluation, NetworkPolicy enforcement
- Color coding: green (allowed), red (blocked), orange (pending), yellow (warning)

#### F-005: AI Mentor
- Always-available AI assistant with Socratic teaching style
- Contextually aware of current mission, current cluster state, user history
- Does NOT give direct answers — asks guiding questions
- Provides "hints" system (3 tiered hints per mission, costs XP)
- Generates personalized explanations with visual callouts in 3D scene
- Tracks knowledge gaps and surfaces review prompts
- Voice mode: text-to-speech explanations synced with 3D animations

#### F-006: Failure Simulation Engine
- Chaos injection library: Node failure, Pod OOM, etcd leader election, network partition, disk full, CrashLoopBackOff, ImagePullBackOff, Pending pods
- User-triggered and auto-triggered failure scenarios
- Difficulty levels: Mild, Moderate, Severe, Catastrophic
- Real-time event log during failures
- Post-mortem auto-generated after mission completion
- "Defend" mission type: prevent failures before they cascade

#### F-007: Gateway API & kgateway Visualization
- Visual representation of Gateway, GatewayClass, HTTPRoute, TCPRoute, TLSRoute
- Traffic flow animation: request → Gateway → HTTPRoute → Backend Service → Pod
- kgateway control plane visualization
- Header matching, path matching, weight-based routing visualized
- TLS termination animated
- Canary deployments via traffic splitting — visual percentage bars
- Policy attachment: visualized policy evaluation chain

#### F-008: Storage Module
- PV, PVC, StorageClass lifecycle animations
- Binding process: PVC → PV matching → binding animation
- Volume mount: Pod to Volume attachment path rendering
- CSI driver visualization
- ReadWriteOnce vs ReadWriteMany access mode demonstration
- StatefulSet + PVC per-pod storage visualization
- Capacity, reclaim policy, and volume expansion animations

#### F-009: Networking Module
- ClusterIP, NodePort, LoadBalancer, ExternalName service types — animated
- kube-proxy iptables/ipvs rule visualization
- DNS resolution path animation (CoreDNS)
- NetworkPolicy: visual firewall rules between namespaces and pods
- CNI plugin simulation (Flannel, Calico modes)
- Ingress controller routing visualization
- CIDR range display on node/pod network interfaces

#### F-010: XP & Progression System
- XP earned for: mission completion, hints not used, speed bonuses, first-time completion, streaks
- Level system: 1–100 with tier names (Explorer → Navigator → Architect → Grandmaster)
- Skill tree: branch into Networking, Storage, Security, Operations, Gateway API
- Weekly XP challenges with bonus multipliers

---

### 3.2 Secondary Features (Should-Have — v1.1)

#### F-011: Achievements & Badges System
- 150+ achievements across categories
- Hidden (secret) achievements for discovery
- Achievement cards shareable to LinkedIn/Twitter/Discord
- Team achievements for enterprise users

#### F-012: Sandbox Mode
- Free-form cluster builder with no mission constraints
- Spawn any K8s resource, configure it, observe behavior
- Share sandbox configurations via permalink
- Import existing YAML to visualize in 3D
- Export configurations as YAML

#### F-013: Community & Social
- Global leaderboard, friend leaderboard, org leaderboard
- Mission replay sharing (record + share your run)
- Community mission SDK — create and publish missions
- Discord integration

#### F-014: Certification Prep Track
- CKA-aligned mission sequences
- CKAD-aligned mission sequences
- CKS-aligned mission sequences (Security module)
- Timed practice exams with simulated environment

#### F-015: Enterprise Features
- SSO via SAML/OIDC
- Custom mission packs
- Team progress dashboards
- Org-level skill gap reports
- Offline mode for air-gapped environments

---

### 3.3 Future Features (Nice-to-Have — v2.0)

#### F-016: Real Cluster Integration
- Connect to real EKS/GKE/AKS clusters
- X-Ray overlay on real cluster data
- Import real cluster state for debugging

#### F-017: Multiplayer Missions
- Cooperative missions (2–4 players manage same cluster)
- Competitive missions (race to fix same failure)

#### F-018: VR/AR Mode
- WebXR support for VR headsets
- AR cluster overlay using device camera

---

## 4. Module Breakdown

### Module 1: Cluster Genesis (Foundation)
**Difficulty:** Beginner | **XP Pool:** 2,000 XP | **Missions:** 18

| Mission | Type | Focus |
|---|---|---|
| 1.1 | Build-It | Create your first cluster, spawn a Node |
| 1.2 | Investigate | Explore Control Plane components |
| 1.3 | Fix-It | Identify unhealthy Node, understand Node conditions |
| 1.4 | Build-It | Deploy your first Pod |
| 1.5 | Investigate | Pod lifecycle: Pending → Running → Succeeded |
| 1.6 | Race | Schedule 10 Pods before timeout |
| 1.7 | Build-It | Create a Namespace, understand isolation |
| 1.8 | Fix-It | Fix a pod stuck in Pending (resource constraints) |
| 1.9 | Investigate | etcd: watch a key write during Pod creation |
| 1.10 | Defend | Keep cluster healthy during random Pod failures |

---

### Module 2: Workloads (Deployments & ReplicaSets)
**Difficulty:** Beginner-Intermediate | **XP Pool:** 3,500 XP | **Missions:** 22

| Mission | Type | Focus |
|---|---|---|
| 2.1 | Build-It | Create Deployment, watch ReplicaSet spawn Pods |
| 2.2 | Investigate | Rolling update: old vs new ReplicaSet competition |
| 2.3 | Fix-It | Deployment stuck in rollout — fix the bad image |
| 2.4 | Build-It | StatefulSet with stable network identity |
| 2.5 | Investigate | DaemonSet: one Pod per Node guarantee |
| 2.6 | Build-It | CronJob: schedule periodic tasks |
| 2.7 | Defend | HPA: survive a traffic surge |
| 2.8 | Fix-It | CrashLoopBackOff — diagnose and fix |
| 2.9 | Build-It | Init Containers: pre-flight checks |
| 2.10 | Race | Zero-downtime rollout with readiness probes |

---

### Module 3: Networking Internals
**Difficulty:** Intermediate | **XP Pool:** 5,000 XP | **Missions:** 25

| Mission | Type | Focus |
|---|---|---|
| 3.1 | Investigate | ClusterIP: how virtual IP works |
| 3.2 | Build-It | NodePort: external access basics |
| 3.3 | Investigate | kube-proxy: iptables rule generation |
| 3.4 | Build-It | DNS resolution: CoreDNS in action |
| 3.5 | Build-It | NetworkPolicy: namespace isolation |
| 3.6 | Fix-It | Pod can't talk to Service — fix the policy |
| 3.7 | Investigate | Endpoints vs EndpointSlices |
| 3.8 | Build-It | Headless Service + StatefulSet DNS |
| 3.9 | Defend | Block an east-west attack via NetworkPolicy |
| 3.10 | X-Ray | Trace a request from client to pod |

---

### Module 4: Gateway API & kgateway
**Difficulty:** Intermediate-Advanced | **XP Pool:** 6,000 XP | **Missions:** 24

| Mission | Type | Focus |
|---|---|---|
| 4.1 | Investigate | Gateway API architecture vs Ingress |
| 4.2 | Build-It | Create GatewayClass and Gateway |
| 4.3 | Build-It | HTTPRoute: path-based routing |
| 4.4 | Build-It | HTTPRoute: header-based routing |
| 4.5 | Build-It | Weight-based traffic splitting (canary) |
| 4.6 | Investigate | kgateway control plane: xDS configuration |
| 4.7 | Build-It | TLS termination at Gateway |
| 4.8 | Build-It | TCPRoute for non-HTTP workloads |
| 4.9 | Fix-It | Misconfigured HTTPRoute — traffic not flowing |
| 4.10 | Defend | Canary rollout under live traffic |
| 4.11 | Build-It | Policy Attachment: rate limiting |
| 4.12 | Build-It | Policy Attachment: authentication |
| 4.13 | X-Ray | Full request trace through Gateway mesh |

---

### Module 5: Storage Deep Dive
**Difficulty:** Intermediate | **XP Pool:** 4,500 XP | **Missions:** 20

| Mission | Type | Focus |
|---|---|---|
| 5.1 | Investigate | PV/PVC lifecycle animation |
| 5.2 | Build-It | Static provisioning: create PV, claim with PVC |
| 5.3 | Build-It | Dynamic provisioning: StorageClass |
| 5.4 | Investigate | CSI driver: watch volume attachment |
| 5.5 | Build-It | StatefulSet: one PVC per Pod |
| 5.6 | Fix-It | Pod stuck in ContainerCreating: PV not bound |
| 5.7 | Investigate | ReadWriteOnce vs ReadWriteMany |
| 5.8 | Build-It | Volume expansion: online resize |
| 5.9 | Fix-It | Data loss scenario: wrong reclaim policy |
| 5.10 | Defend | Survive a storage node failure with replicated PV |

---

### Module 6: Security & RBAC
**Difficulty:** Intermediate-Advanced | **XP Pool:** 5,500 XP | **Missions:** 22

| Mission | Type | Focus |
|---|---|---|
| 6.1 | Investigate | Authentication: certificates, tokens, OIDC |
| 6.2 | Build-It | RBAC: create Role and RoleBinding |
| 6.3 | Fix-It | 403 Forbidden — fix RBAC permissions |
| 6.4 | Build-It | ServiceAccount: application identity |
| 6.5 | Investigate | Pod Security Standards |
| 6.6 | Build-It | Secrets: sealed vs plain secrets |
| 6.7 | Defend | Privilege escalation attack — block it |
| 6.8 | Build-It | OPA/Gatekeeper policy visualization |
| 6.9 | X-Ray | Security X-Ray: trace RBAC evaluation |
| 6.10 | Race | Lock down a cluster before a breach |

---

### Module 7: Observability & Operations
**Difficulty:** Intermediate | **XP Pool:** 4,000 XP | **Missions:** 20

| Mission | Type | Focus |
|---|---|---|
| 7.1 | Investigate | Metrics: CPU/memory graphs on Pods |
| 7.2 | Build-It | HPA: scale on CPU metric |
| 7.3 | Build-It | VPA: automatic resource right-sizing |
| 7.4 | Investigate | Logging pipeline visualization |
| 7.5 | Fix-It | OOMKilled pod — identify and fix limits |
| 7.6 | Build-It | Liveness, Readiness, Startup probes |
| 7.7 | Investigate | Events stream: watch cluster events |
| 7.8 | Defend | Detect and respond to memory leak |
| 7.9 | Build-It | Resource quotas and LimitRanges |
| 7.10 | Race | Diagnose root cause of cascading failure |

---

### Module 8: Failure Simulations (Chaos Lab)
**Difficulty:** Advanced | **XP Pool:** 8,000 XP | **Missions:** 25

| Mission | Type | Chaos Scenario |
|---|---|---|
| 8.1 | Fix-It | Node failure: 1 of 3 nodes goes dark |
| 8.2 | Fix-It | etcd quorum loss: 2 of 3 etcd nodes down |
| 8.3 | Fix-It | Network partition between nodes |
| 8.4 | Fix-It | DNS failure: CoreDNS crashes |
| 8.5 | Fix-It | API server overload: request throttling |
| 8.6 | Fix-It | Disk full: kubelet eviction cascade |
| 8.7 | Fix-It | CrashLoopBackOff: trace root cause |
| 8.8 | Fix-It | ImagePullBackOff: registry unreachable |
| 8.9 | Defend | Prevent cascading failure from one bad deploy |
| 8.10 | Race | Restore cluster quorum in 5 minutes |

---

### Module 9: Advanced Patterns
**Difficulty:** Advanced | **XP Pool:** 7,000 XP | **Missions:** 22

| Mission | Type | Focus |
|---|---|---|
| 9.1 | Build-It | Custom Resources (CRDs) |
| 9.2 | Build-It | Operator pattern: build a mini-operator |
| 9.3 | Build-It | Multi-cluster federation basics |
| 9.4 | Investigate | Cluster autoscaler mechanics |
| 9.5 | Build-It | Admission webhooks |
| 9.6 | Investigate | Scheduler extenders and profiles |
| 9.7 | Build-It | Service mesh sidecar injection |
| 9.8 | Defend | Blue/green deployment with zero downtime |
| 9.9 | Race | Migrate a stateful app across namespaces |
| 9.10 | X-Ray | Trace CRD reconciliation loop |

---

### Module 10: Certification Sprint (CKA/CKAD/CKS)
**Difficulty:** Expert | **XP Pool:** 10,000 XP | **Missions:** 20

| Mission | Type | Cert Alignment |
|---|---|---|
| 10.1–10.7 | Timed Exam | CKA core domains |
| 10.8–10.14 | Timed Exam | CKAD application scenarios |
| 10.15–10.20 | Timed Exam | CKS security hardening |

---

## 5. User Flows

### Flow 1: Onboarding Flow

```
[Landing Page]
     │
     ▼
[Sign Up / OAuth]
     │
     ▼
[Persona Quiz] ← 5 questions: experience, goal, time available
     │
     ├──(Student/Fresher)──► [Guided Path: Module 1 Start]
     │
     ├──(Junior DevOps)────► [Skills Assessment Mission]
     │                              │
     │                         [Place in Module 2 or 3]
     │
     └──(Cloud Engineer)───► [Advanced Entry: Module 3/4]
                                    │
                               [Sandbox Unlocked Immediately]
```

---

### Flow 2: Mission Execution Flow

```
[Mission Select from Learning Path]
         │
         ▼
[Mission Briefing Screen]
 ┌── Story context
 ├── Objectives (numbered)
 ├── Resources available
 └── Estimated time
         │
         ▼
[3D Cluster Loads — Mission State]
         │
         ├── [User performs operations in 3D env]
         │         │
         │         ├── [AI Mentor available — hint button]
         │         ├── [X-Ray Mode toggleable]
         │         └── [Event log streaming]
         │
         ▼
[Auto-Validator runs on objective completion]
         │
         ├── Pass ──► [XP Awarded + Animations] ──► [Debrief]
         │
         └── Fail ──► [Failure Analysis] ──► [Retry or Next Hint]
                              │
                         [Post-Mortem Report generated]
```

---

### Flow 3: X-Ray Mode Flow

```
[Any state in 3D Cluster View]
         │
    [Press X or X-Ray button]
         │
         ▼
[X-Ray Selector Panel]
 ├── Network X-Ray
 ├── Storage X-Ray
 ├── Control Plane X-Ray
 └── Security X-Ray
         │
         ▼
[Overlay renders on existing 3D scene]
         │
         ├── Animated flows appear between objects
         ├── Color-coded paths (green/red/orange)
         ├── Hover any flow to inspect packet/request
         └── Click to freeze and inspect payload
```

---

### Flow 4: Failure Simulation Flow

```
[Chaos Lab — Mission Select or Sandbox]
         │
         ▼
[Chaos Configuration Panel]
 ├── Select failure type
 ├── Select severity
 ├── Select target (Node, Pod, Network, Storage)
 └── Set timer (immediate or scheduled)
         │
         ▼
[Inject Failure → 3D scene animates failure cascade]
         │
         ├── [Pods turn red — CrashLoopBackOff visual]
         ├── [Node grays out — NotReady]
         ├── [Network links break — red animated disconnection]
         └── [Event log floods with errors]
         │
         ▼
[User diagnoses + remedies]
         │
         ▼
[Auto-Validator confirms recovery] ──► [Post-Mortem + XP]
```

---

### Flow 5: AI Mentor Interaction Flow

```
[User stuck / presses AI Mentor button]
         │
         ▼
[AI Mentor Avatar appears (sidebar)]
         │
         ├── [Reads current mission state + cluster state]
         ├── [Reads user's last 3 actions]
         └── [Checks user's knowledge history]
         │
         ▼
[Socratic question: "What do you think the scheduler looks at first?"]
         │
         ├── [User answers] ──► [AI responds with affirmation + deeper question]
         │
         └── [User requests hint] ──► [Tiered hint delivered + XP cost deducted]
                                              │
                                    [Hint 1: conceptual nudge]
                                    [Hint 2: visual callout in 3D]
                                    [Hint 3: near-direct answer]
```

---

### Flow 6: Gateway API Mission Flow

```
[Mission: "Route the Traffic"]
         │
         ▼
[GatewayClass + Gateway objects appear in 3D scene]
         │
         ▼
[User creates HTTPRoute via visual editor or YAML panel]
         │
         ▼
[Traffic flow animation begins]
 ├── Requests flow from external client (animated arrow)
 ├── Hit Gateway (3D gateway object glows)
 ├── HTTPRoute evaluates path/header (rule matching highlighted)
 └── Traffic routed to backend Service → Pod
         │
         ▼
[kgateway xDS push visualized: control plane → data plane sync]
         │
         ▼
[X-Ray Mode: full request trace with timing metrics]
```

---

## 6. Learning Path

### 6.1 Learning Path Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     LEARNING PATH MAP                        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  [ONRAMP] ──► Module 1: Cluster Genesis                     │
│                    │                                         │
│                    ▼                                         │
│              Module 2: Workloads                             │
│                    │                                         │
│          ┌─────────┴──────────┐                             │
│          ▼                    ▼                              │
│    Module 3:           Module 5:                             │
│    Networking          Storage                               │
│          │                    │                              │
│          ▼                    ▼                              │
│    Module 4:           Module 6:                             │
│    Gateway API         Security                              │
│          │                    │                              │
│          └─────────┬──────────┘                             │
│                    ▼                                         │
│              Module 7: Observability                         │
│                    │                                         │
│                    ▼                                         │
│              Module 8: Chaos Lab                             │
│                    │                                         │
│                    ▼                                         │
│              Module 9: Advanced Patterns                     │
│                    │                                         │
│                    ▼                                         │
│              Module 10: Cert Sprint                          │
│                    │                                         │
│                    ▼                                         │
│              [GRANDMASTER]                                   │
└─────────────────────────────────────────────────────────────┘
```

---

### 6.2 Persona-Specific Learning Tracks

#### Track A: "Zero to CKA" (Kai, Priya)
- Duration: 10–12 weeks
- Path: Modules 1 → 2 → 3 → 5 → 6 → 7 → 8 → 10 (CKA)
- Weekly XP target: 800 XP
- Milestones: Weekly checkpoint missions

#### Track B: "DevOps Depth" (Marcus)
- Duration: 6–8 weeks
- Path: Skills Assessment → Modules 3 → 4 → 6 → 8 → 9 → 10
- Skips beginner content via assessment
- Weekly XP target: 1,500 XP

#### Track C: "Gateway & Networking Expert" (Anya)
- Duration: 4–6 weeks
- Path: Modules 3 → 4 → 6 → 9 (focus on 4)
- Sandbox unlocked from day 1
- Certification: CKAD or CKS

---

### 6.3 Weekly Learning Cadence

| Day | Activity | Duration |
|---|---|---|
| Monday | 2 new missions | 45 min |
| Tuesday | X-Ray exploration or sandbox | 30 min |
| Wednesday | 2 new missions | 45 min |
| Thursday | AI Mentor deep dive / review | 20 min |
| Friday | Failure simulation mission | 45 min |
| Saturday | Weekly challenge mission | 60 min |
| Sunday | Leaderboard review / replay | 20 min |

---

### 6.4 Skill Tree

```
                    [Core Operations]
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
    [Networking]      [Storage]       [Security]
          │                │                │
          ▼                ▼                ▼
   [Gateway API]    [Data Services]   [Policy Engine]
          │                │                │
          ▼                ▼                ▼
   [kgateway]      [StatefulApps]    [Zero Trust]
          │
          ▼
   [Service Mesh]
```

Each skill node requires completing associated missions and contributes to a skill profile visible on the user's public profile card.

---

## 7. Gamification System

### 7.1 XP Economy

| Action | XP Earned |
|---|---|
| Mission completion (first time) | 100–500 XP (scales with difficulty) |
| Mission completion (no hints) | +50% bonus XP |
| Mission completion (speed bonus, top 10%) | +25% bonus XP |
| Daily login streak (7 days) | 200 XP |
| Daily login streak (30 days) | 1,000 XP |
| Hint used (Tier 1) | -10 XP |
| Hint used (Tier 2) | -20 XP |
| Hint used (Tier 3) | -40 XP |
| Achievement unlocked | 50–500 XP |
| Weekly challenge | 1,000 XP |
| First sandbox creation | 100 XP |
| Sharing a replay | 25 XP |
| Community upvote received on shared mission | 10 XP |

---

### 7.2 Level System

| Level Range | Tier Name | Badge Color | Unlock |
|---|---|---|---|
| 1–10 | **Explorer** | Gray | Core missions unlocked |
| 11–20 | **Apprentice** | Green | Sandbox Mode unlocked |
| 21–35 | **Navigator** | Blue | Chaos Lab unlocked |
| 36–50 | **Engineer** | Purple | Advanced Patterns unlocked |
| 51–70 | **Architect** | Gold | Community SDK unlocked |
| 71–90 | **Grandmaster** | Platinum | All content unlocked |
| 91–100 | **Legend** | Rainbow/Holographic | Hall of Fame entry |

**XP Thresholds:**

| Level | XP Required (cumulative) |
|---|---|
| 10 | 5,000 XP |
| 20 | 15,000 XP |
| 35 | 40,000 XP |
| 50 | 90,000 XP |
| 70 | 200,000 XP |
| 90 | 450,000 XP |
| 100 | 750,000 XP |

---

### 7.3 Achievement System

#### Category: First Steps (10 achievements)
| Achievement | Trigger | XP |
|---|---|---|
| Hello Kubernetes | Complete Module 1 Mission 1 | 50 |
| Pod Whisperer | Create 50 Pods total | 100 |
| The Scheduler | Manually schedule a Pod | 150 |
| etcd Explorer | Watch 10 etcd operations | 75 |
| Control Tower | Visit all 5 control plane components | 100 |

#### Category: Speed Demon (8 achievements)
| Achievement | Trigger | XP |
|---|---|---|
| Lightning Deploy | Complete a mission in under 2 min | 200 |
| Blitz | Top 1% speed on any mission | 500 |
| No-Hinter | Complete 10 missions without hints | 300 |

#### Category: Chaos Master (12 achievements)
| Achievement | Trigger | XP |
|---|---|---|
| Survived etcd Quorum Loss | Fix etcd in Chaos Lab | 400 |
| The Undertaker | Inject 25 node failures | 250 |
| Phoenix | Restore cluster after total node failure | 500 |
| Butterfly Effect | Trigger cascading failure from 1 bad pod | 300 |

#### Category: Gateway Guru (10 achievements)
| Achievement | Trigger | XP |
|---|---|---|
| Route Master | Create 10 HTTPRoutes | 200 |
| Canary Whisperer | Complete a canary deployment | 250 |
| kgateway Expert | Complete all kgateway missions | 400 |
| Traffic Sculptor | Use all 5 routing rule types | 300 |

#### Category: Secret Achievements (20 achievements — hidden)
Examples:
- **"Ghost in the Shell"** — Trigger: Complete an entire module without opening the UI guide
- **"Time Lord"** — Trigger: Run simulation at 4x speed for 30 minutes
- **"I Read the Docs"** — Trigger: Open the YAML spec view for 50 different resources

---

### 7.4 Leaderboards

| Board Type | Scope | Reset Period |
|---|---|---|
| Global | All users | Weekly |
| Module-specific | All users | Lifetime |
| Friends | User's friend list | Weekly |
| Organization | Enterprise users, same org | Weekly |
| Weekly Challenge | All users | End of challenge |

---

### 7.5 Streaks & Daily Challenges

- **Login Streak**: Tracked daily, multiplier increases XP earned that day
- **Daily Challenge**: One curated 15-minute mission per day, bonus XP
- **Weekly Challenge**: Timed competitive mission, global leaderboard entry
- **Monthly Boss Battle**: Massive multi-objective mission, exclusive cosmetic reward

---

### 7.6 Cosmetics & Customization

- Cluster skins: Neon Cyberpunk, Space Station, Steampunk, Minimalist
- Pod avatar styles: Containers, Robots, Drones, Crystal Orbs
- AI Mentor persona: choose mentor appearance and voice
- Profile card backgrounds (earned via achievements)
- Node nameplate styles

---

## 8. Database Design

### 8.1 Entity Relationship Overview

```
Users ──────────────── UserProgress
  │                         │
  ├── UserAchievements       │
  ├── UserXP_Ledger          │
  ├── UserSkillTree          │
  └── UserSandboxes          │
                             │
Missions ───────────── MissionAttempts
  │                         │
  ├── MissionObjectives      │
  ├── MissionValidator       │
  └── MissionDependencies    │
                             │
Modules ──────────── ModuleProgress
  │
  └── LearningTracks
                        
Achievements ──── AchievementUnlocks
                        
ClusterStates ─── EventLog
  │
  └── SimulationSnapshots
                        
LeaderboardEntries
                        
AIMentorSessions ─── ConversationHistory
```

---

### 8.2 Core Table Schemas

#### Table: `users`
```sql
CREATE TABLE users (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email           VARCHAR(255) UNIQUE NOT NULL,
  username        VARCHAR(50) UNIQUE NOT NULL,
  display_name    VARCHAR(100),
  avatar_url      TEXT,
  hashed_password TEXT,
  oauth_provider  VARCHAR(50),
  oauth_id        VARCHAR(255),
  role            VARCHAR(20) DEFAULT 'learner',
  tier            VARCHAR(20) DEFAULT 'free',
  created_at      TIMESTAMPTZ DEFAULT NOW(),
  last_active_at  TIMESTAMPTZ,
  streak_days     INTEGER DEFAULT 0,
  last_streak_at  DATE,
  org_id          UUID REFERENCES organizations(id),
  persona         VARCHAR(50),
  INDEX (email), INDEX (org_id)
);
```

#### Table: `user_xp_ledger`
```sql
CREATE TABLE user_xp_ledger (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID NOT NULL REFERENCES users(id),
  xp_delta    INTEGER NOT NULL,
  source_type VARCHAR(50) NOT NULL, -- mission, achievement, streak, challenge
  source_id   UUID,
  metadata    JSONB,
  created_at  TIMESTAMPTZ DEFAULT NOW(),
  INDEX (user_id), INDEX (created_at)
);
```

#### Table: `user_levels`
```sql
CREATE TABLE user_levels (
  user_id     UUID PRIMARY KEY REFERENCES users(id),
  total_xp    BIGINT DEFAULT 0,
  level       INTEGER DEFAULT 1,
  tier_name   VARCHAR(50) DEFAULT 'Explorer',
  updated_at  TIMESTAMPTZ DEFAULT NOW()
);
```

#### Table: `modules`
```sql
CREATE TABLE modules (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug            VARCHAR(100) UNIQUE NOT NULL,
  title           VARCHAR(200) NOT NULL,
  description     TEXT,
  difficulty      VARCHAR(20) CHECK (difficulty IN ('beginner','intermediate','advanced','expert')),
  xp_pool         INTEGER,
  order_index     INTEGER,
  prerequisites   UUID[],
  is_active       BOOLEAN DEFAULT true,
  thumbnail_url   TEXT
);
```

#### Table: `missions`
```sql
CREATE TABLE missions (
  id                UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  module_id         UUID NOT NULL REFERENCES modules(id),
  slug              VARCHAR(100) UNIQUE NOT NULL,
  title             VARCHAR(200) NOT NULL,
  type              VARCHAR(30) CHECK (type IN ('fix_it','build_it','investigate','race','defend','x_ray')),
  difficulty        VARCHAR(20),
  story_briefing    TEXT,
  objectives        JSONB NOT NULL, -- [{id, description, validator_fn, order}]
  initial_state     JSONB NOT NULL, -- serialized cluster state
  hints             JSONB,          -- [{tier, content, xp_cost}]
  xp_reward_base    INTEGER,
  time_limit_secs   INTEGER,
  order_index       INTEGER,
  is_active         BOOLEAN DEFAULT true,
  version           INTEGER DEFAULT 1,
  INDEX (module_id)
);
```

#### Table: `mission_attempts`
```sql
CREATE TABLE mission_attempts (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID NOT NULL REFERENCES users(id),
  mission_id      UUID NOT NULL REFERENCES missions(id),
  status          VARCHAR(20) CHECK (status IN ('in_progress','completed','failed','abandoned')),
  started_at      TIMESTAMPTZ DEFAULT NOW(),
  completed_at    TIMESTAMPTZ,
  duration_secs   INTEGER,
  xp_earned       INTEGER DEFAULT 0,
  hints_used      INTEGER DEFAULT 0,
  objectives_completed JSONB, -- [{objective_id, completed_at}]
  score           NUMERIC(5,2),
  cluster_state_log JSONB,  -- event log of user actions
  post_mortem     TEXT,
  INDEX (user_id, mission_id), INDEX (user_id, status)
);
```

#### Table: `achievements`
```sql
CREATE TABLE achievements (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug            VARCHAR(100) UNIQUE NOT NULL,
  title           VARCHAR(200) NOT NULL,
  description     TEXT NOT NULL,
  category        VARCHAR(50),
  xp_reward       INTEGER,
  badge_url       TEXT,
  is_secret       BOOLEAN DEFAULT false,
  trigger_type    VARCHAR(50), -- event-based trigger key
  trigger_config  JSONB,       -- threshold values, conditions
  rarity          VARCHAR(20) CHECK (rarity IN ('common','rare','epic','legendary'))
);
```

#### Table: `user_achievements`
```sql
CREATE TABLE user_achievements (
  user_id         UUID REFERENCES users(id),
  achievement_id  UUID REFERENCES achievements(id),
  unlocked_at     TIMESTAMPTZ DEFAULT NOW(),
  PRIMARY KEY (user_id, achievement_id)
);
```

#### Table: `skill_tree_nodes`
```sql
CREATE TABLE skill_tree_nodes (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug            VARCHAR(100) UNIQUE NOT NULL,
  name            VARCHAR(100) NOT NULL,
  category        VARCHAR(50), -- networking, storage, security, ops, gateway
  parent_node_id  UUID REFERENCES skill_tree_nodes(id),
  xp_required     INTEGER,
  description     TEXT
);
```

#### Table: `user_skill_progress`
```sql
CREATE TABLE user_skill_progress (
  user_id         UUID REFERENCES users(id),
  node_id         UUID REFERENCES skill_tree_nodes(id),
  xp_in_node      INTEGER DEFAULT 0,
  is_unlocked     BOOLEAN DEFAULT false,
  PRIMARY KEY (user_id, node_id)
);
```

#### Table: `cluster_simulation_states`
```sql
CREATE TABLE cluster_simulation_states (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID REFERENCES users(id),
  mission_id      UUID REFERENCES missions(id),
  state_data      JSONB NOT NULL, -- full serialized cluster state
  snapshot_type   VARCHAR(30), -- initial, checkpoint, final, sandbox
  created_at      TIMESTAMPTZ DEFAULT NOW(),
  INDEX (user_id, mission_id)
);
```

#### Table: `ai_mentor_sessions`
```sql
CREATE TABLE ai_mentor_sessions (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID NOT NULL REFERENCES users(id),
  mission_id      UUID REFERENCES missions(id),
  started_at      TIMESTAMPTZ DEFAULT NOW(),
  ended_at        TIMESTAMPTZ,
  conversation    JSONB NOT NULL, -- [{role, content, timestamp}]
  cluster_context JSONB, -- cluster state at session start
  knowledge_gaps  TEXT[]
);
```

#### Table: `leaderboard_snapshots`
```sql
CREATE TABLE leaderboard_snapshots (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  board_type      VARCHAR(30), -- global, module, org, weekly_challenge
  scope_id        UUID,        -- org_id or module_id if scoped
  user_id         UUID NOT NULL REFERENCES users(id),
  score           BIGINT,
  rank            INTEGER,
  period_start    DATE,
  period_end      DATE,
  INDEX (board_type, scope_id, period_start)
);
```

#### Table: `organizations`
```sql
CREATE TABLE organizations (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name            VARCHAR(200) NOT NULL,
  slug            VARCHAR(100) UNIQUE NOT NULL,
  plan            VARCHAR(20) DEFAULT 'enterprise',
  sso_config      JSONB,
  created_at      TIMESTAMPTZ DEFAULT NOW(),
  seat_count      INTEGER DEFAULT 10,
  admin_user_id   UUID REFERENCES users(id)
);
```

---

### 8.3 Data Storage Strategy

| Data Type | Storage | Rationale |
|---|---|---|
| User records, missions, progress | PostgreSQL (primary) | ACID, relational integrity |
| Cluster simulation state | PostgreSQL JSONB + Redis cache | Fast reads during active sessions |
| Real-time simulation events | Redis Pub/Sub + TimescaleDB | Time-series event streaming |
| AI Mentor conversation history | PostgreSQL JSONB | Retrievable context |
| Leaderboard rankings | Redis Sorted Sets + PostgreSQL | Sub-millisecond rank queries |
| Achievement triggers | Redis event queue | Real-time evaluation |
| Session state | Redis | Low-latency session management |
| User-generated content (replays) | S3-compatible object store | Large binary payloads |
| Analytics events | ClickHouse | Columnar, high-volume OLAP |
| CDN assets (3D models, textures) | CloudFront / R2 | Global low-latency delivery |

---

## 9. Technical Architecture

### 9.1 System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                           CLIENT LAYER                               │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │  React 18 + Vite SPA                                         │   │
│  │  ├── Three.js / React Three Fiber (3D Engine)                │   │
│  │  ├── Zustand (Global State)                                   │   │
│  │  ├── React Query (Server State)                               │   │
│  │  ├── Monaco Editor (YAML/JSON editor)                         │   │
│  │  ├── Framer Motion (UI animations)                            │   │
│  │  └── WebSocket client (real-time simulation events)           │   │
│  └──────────────────────────────────────────────────────────────┘   │
└───────────────────────────────┬─────────────────────────────────────┘
                                │ HTTPS / WSS
┌───────────────────────────────▼─────────────────────────────────────┐
│                           API GATEWAY LAYER                          │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │  kgateway (Envoy-based Gateway API implementation)           │   │
│  │  ├── GatewayClass: cloudquest-gateway                        │   │
│  │  ├── HTTPRoute: /api/* → API Services                        │   │
│  │  ├── HTTPRoute: /ws/* → Simulation WebSocket Service         │   │
│  │  ├── HTTPRoute: /ai/* → AI Mentor Service                    │   │
│  │  ├── Rate limiting policy                                     │   │
│  │  ├── JWT authentication policy                               │   │
│  │  └── TLS termination                                         │   │
│  └──────────────────────────────────────────────────────────────┘   │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────────┐
│                         MICROSERVICES LAYER                          │
│                                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │
│  │  Auth        │  │  User        │  │  Mission                 │  │
│  │  Service     │  │  Service     │  │  Service                 │  │
│  │  (Go)        │  │  (Go)        │  │  (Go)                    │  │
│  │  JWT/OIDC    │  │  Profile/XP  │  │  CRUD + Validation       │  │
│  └──────────────┘  └──────────────┘  └──────────────────────────┘  │
│                                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │
│  │  Simulation  │  │  AI Mentor   │  │  Gamification            │  │
│  │  Engine      │  │  Service     │  │  Service                 │  │
│  │  (Go/Rust)   │  │  (Python)    │  │  (Go)                    │  │
│  │  Core Loop   │  │  LLM + RAG   │  │  XP/Achievements/LB      │  │
│  └──────────────┘  └──────────────┘  └──────────────────────────┘  │
│                                                                      │
│  ┌──────────────┐  ┌──────────────────────────────────────────────┐ │
│  │  Analytics   │  │  Notification Service                        │ │
│  │  Service     │  │  (email, in-app, push)                       │ │
│  │  (Go)        │  │  (Go + Kafka consumer)                       │ │
│  └──────────────┘  └──────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────────┐
│                      DATA & MESSAGING LAYER                          │
│                                                                      │
│  PostgreSQL (primary DB)     Redis (cache + sessions + leaderboard)  │
│  TimescaleDB (event stream)  Kafka (event bus)                       │
│  ClickHouse (analytics)      S3/R2 (object storage)                 │
└──────────────────────────────────────────────────────────────────────┘
```

---

### 9.2 Simulation Engine Design

The **Kubernetes Simulation Engine** is the core technical innovation of CloudQuest AI. It is a deterministic, event-driven state machine that models the Kubernetes control plane.

#### Architecture
```
┌─────────────────────────────────────────────────┐
│           SIMULATION ENGINE (Go/Rust)            │
│                                                  │
│  ┌────────────────────────────────────────────┐  │
│  │  State Store (in-memory cluster state)     │  │
│  │  - Nodes, Pods, Deployments, Services...   │  │
│  │  - etcd-like key-value with watch support  │  │
│  └────────────────────────────────────────────┘  │
│                       │                          │
│  ┌────────────────────▼───────────────────────┐  │
│  │  Control Loop Simulator                    │  │
│  │  ├── Scheduler (filter + score + bind)     │  │
│  │  ├── ReplicaSet Controller                 │  │
│  │  ├── Deployment Controller                 │  │
│  │  ├── StatefulSet Controller                │  │
│  │  ├── HPA Controller                        │  │
│  │  ├── Node Controller (heartbeat)           │  │
│  │  └── Kubelet Simulator (per node)          │  │
│  └────────────────────────────────────────────┘  │
│                       │                          │
│  ┌────────────────────▼───────────────────────┐  │
│  │  Event Emitter                             │  │
│  │  - Emits structured events to Kafka topic  │  │
│  │  - Events consumed by WebSocket gateway    │  │
│  │  - Events drive 3D animation triggers      │  │
│  └────────────────────────────────────────────┘  │
│                       │                          │
│  ┌────────────────────▼───────────────────────┐  │
│  │  Chaos Injector                            │  │
│  │  - Node failure, network partition         │  │
│  │  - OOM injection, disk full                │  │
│  │  - Pluggable chaos providers               │  │
│  └────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

#### Simulation Fidelity Levels

| Level | Description | Use Case |
|---|---|---|
| **Schematic** | Object relationships only, no timing | Beginner missions |
| **Behavioral** | State transitions + basic timing | Most missions |
| **High-Fidelity** | Full control loop timing, scheduling scores visible | X-Ray Mode, advanced missions |
| **Chaos** | Probabilistic failures, race conditions | Chaos Lab |

---

### 9.3 3D Visualization Engine

**Technology Stack:**
- Three.js + React Three Fiber (WebGL rendering)
- GLSL custom shaders for energy flow animations
- GSAP for UI animation timeline control
- R3F Drei for helpers (OrbitControls, Instances, Text3D)

**Rendering Architecture:**
```
Scene Graph
├── ClusterEnvironment (skybox, ground, ambient light)
├── ControlPlane (elevated platform)
│   ├── APIServerObject (glowing monolith)
│   ├── SchedulerObject (animated decision tree)
│   ├── ControllerManagerObject (spinning gears)
│   └── etcdObject (crystal data store)
├── NodeGroup[]
│   ├── NodeRack (physical server visual)
│   └── PodContainer[] (animated pod objects)
│       ├── ContainerVisual
│       ├── StatusIndicator (pulsing halo)
│       └── ResourceGauge (CPU/memory bars)
├── NetworkLayer
│   ├── ServiceMeshLines (animated particle flow)
│   ├── GatewayObject
│   └── IngressObject
├── StorageLayer
│   ├── PVObject (disk visual)
│   ├── PVCBindingAnimation
│   └── MountPathLines
└── XRayOverlay (toggleable)
    ├── NetworkFlowParticles
    ├── PacketInspector
    └── PolicyEnforcementZones
```

**Performance Targets:**
- 60 FPS on integrated GPU (Intel Iris Xe, Apple M1)
- 30 FPS minimum on budget laptops
- Instance merging for large pod counts (100+ pods)
- LOD (Level of Detail) for distant objects

---

### 9.4 AI Mentor Architecture

```
┌────────────────────────────────────────────────────┐
│               AI MENTOR SERVICE (Python)            │
│                                                     │
│  ┌───────────────────────────────────────────────┐  │
│  │  Context Builder                              │  │
│  │  ├── Current mission state                   │  │
│  │  ├── User's last N actions (from sim engine) │  │
│  │  ├── User knowledge profile (from DB)        │  │
│  │  └── Current cluster state snapshot          │  │
│  └─────────────────────┬─────────────────────────┘  │
│                        │                            │
│  ┌─────────────────────▼─────────────────────────┐  │
│  │  RAG Pipeline                                 │  │
│  │  ├── Vector DB: Kubernetes docs + CNCF specs  │  │
│  │  ├── Mission knowledge base                   │  │
│  │  └── User history summaries                  │  │
│  └─────────────────────┬─────────────────────────┘  │
│                        │                            │
│  ┌─────────────────────▼─────────────────────────┐  │
│  │  LLM (Gemini 2.5 Pro / Claude 3.7 Sonnet)    │  │
│  │  System prompt: Socratic teaching mode        │  │
│  │  Tool calls: highlight_3d_object(), zoom_to() │  │
│  └─────────────────────┬─────────────────────────┘  │
│                        │                            │
│  ┌─────────────────────▼─────────────────────────┐  │
│  │  Response Processor                           │  │
│  │  ├── Extract 3D callout commands              │  │
│  │  ├── Format for UI rendering                  │  │
│  │  └── Update knowledge gap tracker            │  │
│  └───────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────┘
```

**AI Mentor Personality Modes:**
- **Guide Mode**: Socratic questioning, never gives direct answers
- **Explain Mode**: Triggered by user request, detailed explanations with 3D sync
- **Challenge Mode**: Poses harder questions, rewards deep thinking
- **Emergency Mode**: When user is stuck for >10 min, provides more direct guidance

---

### 9.5 Gateway API / kgateway Integration

The platform itself is deployed using Kubernetes Gateway API with **kgateway** as the implementation — making the technology the platform teaches the same technology it runs on.

**Production Deployment GatewayClass:**
```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: GatewayClass
metadata:
  name: cloudquest-kgateway
spec:
  controllerName: kgateway.dev/kgateway

---
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: cloudquest-gateway
  namespace: cloudquest-system
spec:
  gatewayClassName: cloudquest-kgateway
  listeners:
    - name: https
      protocol: HTTPS
      port: 443
      tls:
        certificateRefs:
          - name: cloudquest-tls-cert
    - name: websocket
      protocol: HTTPS
      port: 443

---
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: api-route
spec:
  parentRefs:
    - name: cloudquest-gateway
  rules:
    - matches:
        - path:
            type: PathPrefix
            value: /api
      backendRefs:
        - name: api-service
          port: 8080
    - matches:
        - path:
            type: PathPrefix
            value: /ai
      backendRefs:
        - name: ai-mentor-service
          port: 8000
```

---

### 9.6 Storage Architecture

| Component | Technology | Purpose |
|---|---|---|
| Primary Database | PostgreSQL 16 (HA cluster) | All relational data |
| Cache | Redis 7 Cluster | Sessions, leaderboard, hot data |
| Time-series | TimescaleDB | Simulation event streams |
| Object Storage | Cloudflare R2 | 3D assets, replay recordings |
| Search | Elasticsearch | Mission search, knowledge base |
| Analytics | ClickHouse | User behavior OLAP |
| Message Bus | Apache Kafka | Inter-service events |
| Secrets | HashiCorp Vault | API keys, certificates |

---

### 9.7 Infrastructure

- **Cloud Provider:** Multi-cloud (primary GCP, secondary AWS)
- **Container Orchestration:** Kubernetes (GKE Autopilot)
- **Service Mesh:** Istio (observability layer)
- **CI/CD:** GitHub Actions → ArgoCD (GitOps)
- **IaC:** Terraform + Helm
- **Observability:** Prometheus + Grafana + Jaeger + Loki
- **CDN:** Cloudflare
- **DNS:** Cloudflare DNS

---

### 9.8 Security Architecture

| Layer | Control |
|---|---|
| Identity | JWT + OIDC, MFA support |
| Transport | TLS 1.3 everywhere |
| API | Rate limiting via kgateway policy, DDoS protection via Cloudflare |
| Container | Pod Security Standards (restricted), read-only root FS |
| Network | NetworkPolicy, namespace isolation per service |
| Secrets | Vault-injected via sidecar, never in env vars |
| Data | Encryption at rest (AES-256), GDPR data export/delete |
| RBAC | Least-privilege service accounts per microservice |

---

## 10. Development Roadmap

### Phase 1: Foundation (Months 1–4)
**Goal:** Working MVP with core loop playable

#### Sprint 1-2 (Month 1): Infrastructure & Auth
- [ ] Kubernetes cluster setup (GKE) with kgateway
- [ ] Auth Service (JWT, Google OAuth, GitHub OAuth)
- [ ] User Service (profile, XP ledger)
- [ ] PostgreSQL + Redis setup
- [ ] CI/CD pipeline (GitHub Actions + ArgoCD)
- [ ] Basic React + Vite frontend skeleton

#### Sprint 3-4 (Month 2): Simulation Engine Core
- [ ] Simulation Engine v0.1 (Pod scheduling, ReplicaSet controller)
- [ ] In-memory state store
- [ ] WebSocket event streaming
- [ ] Basic cluster state serialization/deserialization
- [ ] Kubelet simulator (pod lifecycle states)

#### Sprint 5-6 (Month 3): 3D Visualization Engine
- [ ] Three.js scene setup with React Three Fiber
- [ ] Node rack and Pod object rendering
- [ ] Control Plane visualization (API server, scheduler, etcd, CM)
- [ ] Basic camera controls (orbit, zoom, focus)
- [ ] Object inspector (click → show spec panel)
- [ ] WebSocket → 3D event consumer (state changes → animations)

#### Sprint 7-8 (Month 4): Mission System v1 + Module 1
- [ ] Mission Service (CRUD, validator framework)
- [ ] Mission execution flow (briefing → sandbox → validate → debrief)
- [ ] Module 1: Cluster Genesis — all 18 missions authored
- [ ] XP system v1 (earn, track, display)
- [ ] Basic level system (1–10)

**Phase 1 Milestone:** Internal playtest — Modules 1 complete, 10 staff testers

---

### Phase 2: Core Experience (Months 5–8)
**Goal:** Shipping v1.0 with Modules 1–5, AI Mentor, X-Ray Mode

#### Month 5: AI Mentor + Modules 2–3
- [ ] AI Mentor Service (Python, Gemini API integration)
- [ ] RAG pipeline with Kubernetes docs
- [ ] Context-aware Socratic response system
- [ ] 3D callout commands from AI Mentor
- [ ] Module 2: Workloads (Deployments) — 22 missions
- [ ] Module 3: Networking — first 15 missions

#### Month 6: X-Ray Mode + Storage Module
- [ ] X-Ray Mode infrastructure (overlay rendering system)
- [ ] Network X-Ray (packet flow visualization)
- [ ] Storage X-Ray (PV/PVC binding animation)
- [ ] Module 5: Storage — 20 missions
- [ ] Complete Module 3 Networking — remaining 10 missions

#### Month 7: Gateway API Module + kgateway Visualization
- [ ] Gateway API object rendering (Gateway, GatewayClass, HTTPRoute)
- [ ] Traffic flow animation engine
- [ ] kgateway xDS sync visualization
- [ ] Module 4: Gateway API — 24 missions
- [ ] Canary deployment visual

#### Month 8: Gamification + Achievements + Beta Launch
- [ ] Achievement system (150 achievements)
- [ ] Leaderboards (global, module, weekly)
- [ ] Streak system + daily challenges
- [ ] Profile cards + social sharing
- [ ] Beta launch (invite-only, 500 users)

**Phase 2 Milestone:** Public Beta — v1.0-beta, Modules 1–5, 500 beta users

---

### Phase 3: Advanced Modules + GA (Months 9–12)
**Goal:** Public GA with full module set, enterprise features

#### Month 9: Security Module + Failure Simulations
- [ ] Module 6: Security & RBAC — 22 missions
- [ ] Security X-Ray (RBAC evaluation trace)
- [ ] Chaos Injector framework
- [ ] Module 8: Chaos Lab — first 15 missions

#### Month 10: Observability Module + Advanced Patterns
- [ ] Module 7: Observability — 20 missions
- [ ] Control Plane X-Ray
- [ ] Module 9: Advanced Patterns — 22 missions
- [ ] Operator pattern visualization
- [ ] CRD reconciliation loop X-Ray

#### Month 11: Cert Tracks + Sandbox Mode + Community
- [ ] Module 10: Cert Sprint — 20 missions (CKA/CKAD/CKS)
- [ ] Sandbox Mode (free-form cluster builder)
- [ ] Community mission SDK (alpha)
- [ ] Complete Chaos Lab Module 8 — all 25 missions
- [ ] Replay recording + sharing

#### Month 12: Enterprise Features + GA
- [ ] SSO (SAML/OIDC)
- [ ] Org leaderboards + team dashboards
- [ ] Custom mission packs for enterprise
- [ ] Skill gap reports
- [ ] Performance optimization (60 FPS guarantee)
- [ ] GDPR compliance audit
- [ ] **General Availability Launch**

**Phase 3 Milestone:** GA Launch — full platform, enterprise tier, all 10 modules

---

### Phase 4: Growth & Platform (Year 2)

| Quarter | Focus | Key Deliverables |
|---|---|---|
| Q1 Y2 | Real Cluster Integration | EKS/GKE/AKS connect, import real cluster |
| Q2 Y2 | Multiplayer Missions | Co-op + competitive modes |
| Q3 Y2 | Community Ecosystem | Open mission marketplace, SDK GA |
| Q4 Y2 | VR/AR Mode | WebXR support, AR overlay |

---

### Resource Plan

| Phase | Engineering Team | Notes |
|---|---|---|
| Phase 1 | 3 engineers | 2 backend (Go), 1 fullstack (React/Three.js) |
| Phase 2 | 6 engineers | +1 AI/ML (Python), +1 3D (Three.js), +1 backend |
| Phase 3 | 9 engineers | +2 backend, +1 DevOps/Platform |
| Phase 4 | 12 engineers | +3 features/community |

**Non-Engineering:**
- 1 Product Designer (full-time from Phase 1)
- 1 Content Architect (mission authoring, from Phase 2)
- 1 DevOps/SRE (from Phase 2)
- 1 AI Prompt Engineer (from Phase 2)

---

### Technology Stack Summary

| Layer | Technology |
|---|---|
| Frontend | React 18, Vite, Three.js, React Three Fiber, Framer Motion, Zustand |
| 3D Engine | Three.js, WebGL, GLSL shaders, GSAP, R3F Drei |
| API Gateway | Kubernetes Gateway API + kgateway |
| Backend Services | Go (primary), Python (AI Mentor) |
| Database | PostgreSQL 16, Redis 7, TimescaleDB, ClickHouse |
| Messaging | Apache Kafka |
| Object Storage | Cloudflare R2 |
| AI | Gemini 2.5 Pro, vector embeddings, RAG |
| Infrastructure | GKE, Terraform, Helm, ArgoCD |
| Observability | Prometheus, Grafana, Jaeger, Loki |
| Security | Vault, Istio, kgateway policies |

---

*Document Version: 1.0 | Last Updated: June 2026*  
*Author: Principal Product Architect | CloudQuest AI*

---

> **"The best way to learn Kubernetes is to live inside it."**
