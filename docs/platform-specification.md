# Games of 42
## Platform Specification v0.1

---

# 1. Overview

Games of 42 is a real-time moderated challenge engine designed for structured live experiences.

The platform consists of two primary components:

1. Player Application (mobile-first, embedded within H2GE Guides)
2. GameRunner Console (web-based live session control system)

The system is event-driven and safety-first, with AI-assisted challenge evaluation.

---

# 2. System Architecture

## 2.1 High-Level Components

- Player Application (Mobile / Web)
- GameRunner Console (Web SPA)
- Backend API
- Real-Time Event Layer (WebSockets)
- AI Safety Evaluation Service
- Database Layer

## 2.2 Proposed Stack

- Backend: Node.js or Python
- Database: PostgreSQL
- Session Cache: Redis
- Real-Time: WebSockets
- Frontend: React / React Native
- AI Integration: API-based evaluation service

---

# 3. Core Design Constraint

The system includes a configurable constant:

coreNumber = 42

Default uses:
- 42-minute sessions
- Up to 42 players per session
- 42-point scoring logic
- 42-based badge or milestone systems

The value must be configurable but default to 42.

---

# 4. Player Application

## 4.1 Functional Requirements

- Join active session
- View active challenge
- Submit challenge completion
- Propose new challenge
- Communicate with GameRunner
- Receive alerts and updates
- Track progress and points

## 4.2 Player Data Model

```json
{
  "playerId": "UUID",
  "displayName": "String",
  "status": "online | offline | inSession",
  "totalPoints": 0,
  "completedChallenges": 0,
  "activeSessionId": "UUID",
  "preferences": {
    "maxPhysicalIntensity": 0,
    "locationSharing": true
  }
}

# 5. GameRunner Console

The GameRunner Console is a web-based control center for moderating and operating live sessions in real time. It provides operational control, player monitoring, communications, and AI-assisted evaluation.

## 5.1 Primary Console Modules

### 5.1.1 Session Control
- Create session
- Start / pause / resume / end session
- Set session duration (default: 42 minutes)
- Set player cap (default: 42)
- Assign active challenge
- Emergency stop (challenge-level and session-level)
- Live modification controls (time, difficulty, constraints)

### 5.1.2 Challenge Approval Workflow
- View proposed challenges (queue)
- Review AI screening results
- Approve / reject / request modifications
- Edit challenge details before approval
- Push approved challenge to “live” session
- Track challenge version history

### 5.1.3 Live Player Monitoring
- Player list and status (online/offline/in-session)
- Player location status (if enabled)
- Completion submissions and timestamps
- Safety flags and alerts
- Remove player from session (with reason logging)

### 5.1.4 Communication Hub
- Broadcast announcements to all players
- Send direct messages to individual players
- Send team messages (if teams enabled)
- Trigger emergency alerts
- Log all messages for audit

### 5.1.5 AI Assistance Panel
- Challenge safety evaluation summary
- Similar challenge detection
- Balance checking (difficulty, duration, fairness)
- Location suitability prompts
- Recommended modifications (auto-suggested edits)

## 5.2 Console Functional Requirements

- Real-time updates of session state
- Real-time player event stream (joins, leaves, completions, alerts)
- One-click emergency pause/stop
- Audit logging of all critical actions:
  - approvals
  - edits
  - overrides
  - removals
  - emergency actions
- Role-based permissions (Runner vs Admin)

## 5.3 Runner Data Model

```json
{
  "runnerId": "UUID",
  "name": "String",
  "status": "active | break | planning",
  "currentSessions": [
    {
      "sessionId": "UUID",
      "playerCount": 0,
      "activeChallengeId": "UUID",
      "status": "live | paused | ended"
    }
  ],
  "permissions": {
    "overrideAI": true,
    "maxPlayers": 42,
    "maxChallengeRiskLevel": 3
  },
  "aiAssistant": {
    "preferredSettings": {},
    "savedResponses": [],
    "customRules": []
  }
}
