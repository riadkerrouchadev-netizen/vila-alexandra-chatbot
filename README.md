# Vila Alexandra — AI Booking Assistant 🏨

A multilingual AI-powered booking assistant built for a hospitality business. Handles guest inquiries, room availability, and reservation management in 6 languages — running 24/7 on a dedicated server.

## Results

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Profit | baseline | — | **+83% YoY** |
| Direct bookings | baseline | — | **+60% YoY** |
| Response time | hours | seconds | **~instant** |
| Languages supported | 1 | 6 | **6x coverage** |

## Features

- **Multilingual support** — English, French, Portuguese, Spanish, German, Italian
- **Natural conversation** — Guests interact naturally, the bot understands context and intent
- **Booking management** — Check availability, suggest rooms, handle reservations
- **WhatsApp integration** — Meets guests where they already are
- **24/7 availability** — No missed inquiries, instant responses at any hour
- **Handoff to human** — Escalates complex requests to staff seamlessly

## Architecture

```
Guest (WhatsApp)
    │
    ▼
┌─────────────────────┐
│   FastAPI Backend    │
│   ├── Message router │
│   ├── Language detect│
│   └── Session mgmt  │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│   AI Engine          │
│   ├── OpenAI API     │
│   ├── Context builder│
│   └── Response gen   │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│   Data Layer         │
│   ├── Room inventory │
│   ├── Booking DB     │
│   └── Guest history  │
└─────────────────────┘
```

## Tech Stack

- **Backend**: Python, FastAPI
- **AI**: OpenAI API, custom prompt engineering
- **Database**: PostgreSQL
- **Messaging**: WhatsApp Business API
- **Deployment**: Docker, Hetzner VPS
- **Monitoring**: Custom logging, health checks

## Key Design Decisions

**Why FastAPI over Flask?** Async support was critical — the bot handles concurrent conversations from multiple guests in different languages. FastAPI's native async + Pydantic validation made the message pipeline robust.

**Why not a chatbot framework?** Frameworks like Rasa or Botpress add complexity without flexibility. A custom pipeline with direct OpenAI API calls gave full control over prompt engineering, language switching, and booking logic.

**Session management**: Each guest gets a conversation context window. The bot remembers what was discussed within a session, enabling natural multi-turn conversations ("What about the room you mentioned earlier?").

## Deployment

Dockerized and running on a Hetzner VPS. The container auto-restarts on failure, with health check endpoints monitored externally.

```bash
docker build -t vila-bot .
docker run -d --restart unless-stopped -p 8000:8000 --env-file .env vila-bot
```

---

> **Note**: This is a showcase repository. The actual production code is proprietary. This repo demonstrates the architecture, approach, and results of the project.
