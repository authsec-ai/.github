# AuthSec

**AuthSec** is an **Agent-Native Authentication and Authorization platform** designed for AI agents, MCP servers, and modern applications.

It provides identity, authentication, authorization, secrets, and workload identity for autonomous systems and services.

---

## What AuthSec Enables

- 🔐 **Agent authentication** using OIDC / SAML2 SSO  
- 🤖 **Headless authentication** using CIBA  
- 🛡 **RBAC authorization** for AI agents and services  
- 🔑 **Secure secrets storage and retrieval**  
- 🔗 **SPIFFE workload identity integration**  
- 👥 **Multi-tenant IAM platform**  
- 🔑 **Passkeys / WebAuthn MFA**

---

# Installation

AuthSec consists of two main components:

| Component | Repository |
|---|---|
| Backend API | https://github.com/authsec-ai/authsec |
| Web Console | https://github.com/authsec-ai/authsec-ui |

Both services must be running.

---

# 1. Run AuthSec Backend

### Requirements

- Go **1.25+**
- PostgreSQL **14+**
- (Optional) Redis
- (Optional) HashiCorp Vault

---

### Clone the repository

```bash
git clone https://github.com/authsec-ai/authsec.git
cd authsec
```

---

### Configure environment

```bash
cp .env.example .env
```

Minimum configuration:

```env
DB_NAME=authsec_db
DB_USER=authsec
DB_PASSWORD=password
DB_HOST=localhost
DB_PORT=5432

WEBAUTHN_RP_NAME=AuthSec
WEBAUTHN_RP_ID=localhost
WEBAUTHN_ORIGIN=http://localhost:5173
```

---

### Run the server

```bash
go run ./cmd/
```

AuthSec will start on:

```
http://localhost:7468
```

Health check:

```bash
curl http://localhost:7468/authsec/uflow/health
```

---

# 2. Run AuthSec UI

### Requirements

- Node.js **20+**
- npm **10+**

---

### Clone the repository

```bash
git clone https://github.com/authsec-ai/authsec-ui.git
cd authsec-ui
```

---

### Install dependencies

```bash
npm install
```

---

### Configure environment

```bash
cp .env.example .env
```

Edit `.env`:

```env
VITE_API_URL=http://localhost:7468
VITE_APP_NAME=AuthSec
```

---

### Start the UI

```bash
npm run dev
```

UI will be available at:

```
http://localhost:5173
```

---

# Architecture

```
        +----------------------+
        |      AuthSec UI      |
        |   React + Vite + TS  |
        +----------+-----------+
                   |
                   |
        +----------v-----------+
        |      AuthSec API     |
        |        Go + Gin      |
        +----------+-----------+
                   |
     +-------------+-------------+
     |             |             |
 PostgreSQL      Redis         Vault
```

---

# Hosted Platform

If you prefer not to self-host AuthSec, you can use the managed platform:

**https://app.authsec.ai**

---

# Repositories

| Repository | Description |
|---|---|
| https://github.com/authsec-ai/authsec | Core IAM backend |
| https://github.com/authsec-ai/authsec-ui | Web console |
| https://github.com/authsec-ai/sdk-authsec | SDK for agents and services |

---

# License

Apache License 2.0
