# Safeguardly — System Architecture

## Overview
Safeguardly is designed as a multi-tier platform:
- **Client layer:** Mobile App + Web Dashboard.
- **API layer:** Backend services handling authentication, alerts, and analytics.
- **Data layer:** PostgreSQL for persistence and Redis for fast queues.
- **Realtime layer:** WebSocket / Firebase for live updates.
- **Notification layer:** Twilio (SMS) and FCM (push).

---

## Component breakdown

### 1. Frontend
- **Mobile app:** One-tap SOS, location broadcast, and history log.
- **Web dashboard:** View live incidents, assign responders, mark resolutions.
- **Stack:** React Native + React JS consuming REST API endpoints.

### 2. Backend (API)
- Built with **Node.js + Express**.
- Core modules:
  - **Auth:** JWT-based login, two-factor for admins.
  - **Incident:** CRUD + websocket broadcast.
  - **Notification:** Queue handler → SMS, Push, Email.
  - **Analytics:** Aggregates incident data for reporting.

### 3. Database
| Table | Purpose |
|--------|----------|
| users | profile, roles (user, responder, admin) |
| incidents | id, user_id, type, location, status |
| responders | contact details, duty schedule |
| notifications | logs of messages sent |
| feedback | user satisfaction & post-incident review |

### 4. Realtime & Notification Flow
```mermaid
sequenceDiagram
  participant U as User
  participant API as Backend
  participant WS as WebSocket
  participant R as Responder
  U->>API: Trigger SOS
  API->>WS: Broadcast incident
  WS->>R: Push live alert
  API->>Twilio: Send SMS fallback
  R->>API: Acknowledge & update status
  API->>U: Notify "help en route"
  
