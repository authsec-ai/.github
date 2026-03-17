# AuthSec

**AuthSec** is an **Agent-Native Authentication and Authorization platform** designed for **AI agents, MCP servers, and modern applications**.

It provides identity, authentication, authorization, secrets management, and workload identity for autonomous systems and services.

---

## What AuthSec Enables

- 🔐 **Agent authentication** using OIDC / SAML2 SSO  
- 🤖 **Headless authentication** using CIBA  
- 🛡 **RBAC authorization** for AI agents and services  
- 🔑 **Secrets storage and retrieval**  
- 🔗 **SPIFFE workload identity**  
- 👥 **Multi-tenant IAM platform**  
- 🔑 **Passkeys / WebAuthn MFA**

---

# Installation

AuthSec consists of two main components:

| Component | Repository |
|---|---|
| Backend API | https://github.com/authsec-ai/authsec-ai |
| Web Console | https://github.com/authsec-ai/authsec-ui |

Both services must be running.

---

# 1. Run AuthSec Backend

### Requirements

- Go **1.25+**
- PostgreSQL **14+**
- (Optional) Redis
- (Optional) HashiCorp Vault

### Clone repository

```bash
git clone https://github.com/authsec-ai/authsec-ai.git
cd authsec
```

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

### Run the backend

```bash
go run ./cmd/
```

AuthSec backend will start on:

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

### Clone repository

```bash
git clone https://github.com/authsec-ai/authsec-ui.git
cd authsec-ui
```

### Install dependencies

```bash
npm install
```

### Configure environment

```bash
cp .env.example .env
```

Edit `.env`:

```env
VITE_API_URL=http://localhost:7468
VITE_APP_NAME=AuthSec
```

### Start UI

```bash
npm run dev
```

The UI will be available at:

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

# Documentation

Full documentation is available at:

👉 https://docs.authsec.dev/getting-started/

The documentation includes:

- Platform overview
- Authentication setup
- RBAC configuration
- AI agent authentication
- SPIFFE workload identity
- Security best practices
- Integration guides

---

# Open Source Documentation

AuthSec documentation is open source and maintained in the following repositories.

| Repository | Description |
|---|---|
| https://github.com/authsec-ai/authsec-community-docs | Platform documentation |
| https://github.com/authsec-ai/authsec-community-apidocs | API reference documentation |

Developers can update documentation when contributing features.

---

# Updating Docs Locally

If you are contributing to AuthSec and want to update the documentation alongside your code changes:

### Platform Documentation

```bash
git clone https://github.com/authsec-ai/authsec-community-docs.git
cd authsec-community-docs
```

Follow the instructions in that repository to run the docs locally and submit a pull request with your changes.

---

### API Documentation

```bash
git clone https://github.com/authsec-ai/authsec-community-apidocs.git
cd authsec-community-apidocs
```

Update API specs and examples according to your changes before submitting a pull request.

---

# Hosted Platform

If you prefer not to self-host AuthSec, you can use the managed platform:

👉 https://authsec.ai

---

# Repositories

| Repository | Description |
|---|---|
| https://github.com/authsec-ai/authsec-ai | Core IAM backend |
| https://github.com/authsec-ai/authsec-ui | Web console |
| https://github.com/authsec-ai/sdk-authsec | SDK for agents and services |
| https://github.com/authsec-ai/authsec-community-docs | Documentation |
| https://github.com/authsec-ai/authsec-community-apidocs | API documentation |

---

# License

Apache License 2.0
