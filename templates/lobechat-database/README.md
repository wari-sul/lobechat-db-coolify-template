# LobeChat Database (Decoupled Deployment)

<!-- ![LobeChat Banner](../../cover-pages/lobechat-banner.png) -->

## Overview

This Docker Compose deploys **LobeChat Database** with **pgvector** in a single stack, while using **separate/decoupled** Logto (auth) and MinIO (S3) stacks. All services communicate via Coolify proxy/magic URLs.

## Architecture

```
Stack A: Logto (+ own Postgres)    → https://logto.example.com
Stack B: MinIO S3                 → https://s3.example.com  
Stack C+D: pgvector + LobeChat    → https://chat.example.com
```

## Deployment Steps

### 1. Prerequisites (already deployed)
- **Stack A**: Logto Console → Applications → Create OIDC app → copy `client_id`/`client_secret`
- **Stack B**: MinIO → create bucket (e.g. `lobe`) → create access key → note public domain

### 2. Deploy this compose (Stack C+D)
1. Coolify → New → Docker Compose → paste YAML
2. **Environment Variables** (all required):
```
POSTGRES_USER=postgres
POSTGRES_PASSWORD=strongpassword123

LOBECHAT_PUBLIC_URL=https://chat.example.com
OPENAI_API_KEY=sk-...

S3_ENDPOINT=https://s3.example.com
S3_BUCKET=lobe
S3_PUBLIC_DOMAIN=https://s3.example.com
S3_ACCESS_KEY_ID=your-minio-key
S3_SECRET_ACCESS_KEY=your-minio-secret

AUTH_LOGTO_ISSUER=https://logto.example.com/oidc
AUTH_LOGTO_ID=<from Logto app>
AUTH_LOGTO_SECRET=<from Logto app>

KEY_VAULTS_SECRET=$(openssl rand -base64 32)
NEXT_AUTH_SECRET=$(openssl rand -base64 32)
```
3. **Lobechat service → Domains**: `https://chat.example.com:3210`
4. Deploy

## Coolify Magic Vars Used

- `POSTGRES_*` → shared between pgvector + LobeChat DB URL
- `${LOBECHAT_PUBLIC_URL}/api/auth` → auto-generates correct NextAuth callback

## Logto Configuration (in Logto Console)

For the LobeChat OIDC app:
```
Redirect URIs: https://chat.example.com/api/auth/callback/logto
Post sign-out: https://chat.example.com
```

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `ENOTFOUND pgvector` | pgvector + LobeChat must be **same compose** |
| `no available server` | Lobechat service Domains = `https://chat.example.com:3210` |
| `/api/auth/error "Bad request"` | `NEXTAUTH_URL=${LOBECHAT_PUBLIC_URL}/api/auth` (note the `/`) |

## Scaling Notes

- **pgvector**: Single instance (add replicas if needed)
- **MinIO**: Scale horizontally if >1TB storage
- **Logto**: Already decoupled, scales independently

**Success**: LobeChat loads → Logto login → dashboard works → AI chat functional.
