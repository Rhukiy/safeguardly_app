# Safeguardly System Architecture ⚙️

## Overview
Safeguardly uses a layered architecture — frontend, backend, and data systems — connected via REST APIs and WebSocket channels for real-time safety coordination.

## Frontend Stack
- **User App:** Flutter (cross-platform mobile)
- **Responder App:** Flutter (limited admin functions)
- **Admin Dashboard:** React + Tailwind CSS
- **Authentication:** JWT via Auth0

## Backend Stack
- **API Gateway:** Node.js (Express) — entry point for SOS & system events  
- **Incident Service:** Handles creation, validation, and routing of incidents  
- **Notification Queue:** Redis Pub/Sub for push & SMS job queues  
- **Realtime Service:** WebSocket server (Socket.io) for live location updates  
- **Verification Service:** Manages staged KYC & responder validation  
- **Audit Logger:** Append-only log service for compliance

## Database & Infrastructure
| Layer | Technology | Purpose |
|--------|-------------|----------|
| Relational DB | PostgreSQL | Incidents, users, org data |
| Cache/Queue | Redis | Queue jobs & sessions |
| Object Storage | AWS S3 | Media & documents |
| Notifications | Twilio SMS / Firebase FCM | Alerts |
| Monitoring | Grafana + ELK | System logs & uptime |

## Communication Flow
1. **User triggers SOS** → API Gateway.  
2. **Incident Service** creates record, sends to Queue.  
3. **Notification Service** dispatches push/SMS.  
4. **Realtime Service** streams to Dashboard & Responders.  
5. **Responder updates status**, synced live via WebSocket.  
6. **Audit Logger** stores all actions for analytics.

## Feasibility
- Uses **scalable, open-source tools** with proven reliability.  
- Works offline via **SMS fallback**.  
- Modular microservice pattern allows scaling different modules independently.  
- Security ensured via **role-based access** and **JWT auth**.

