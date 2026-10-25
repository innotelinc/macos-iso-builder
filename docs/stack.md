# macOS ISO Builder in the Innotel Platform Stack

**Role: BuilderOps** — Build bootable macOS installer ISOs and DMGs from Apple's servers.

Part of the [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack).
The canonical definition of the stack, its shared layers and their owners lives
there; this file records only what macOS ISO Builder does inside it.

## Boundaries

### Owns

- the mkmaciso script
- the ISO and DMG build
- the GitHub Actions workflows

### Consumes

- Apple's installer servers
- macOS built-in tools and hosted Mac runners
- Cerulean Vault (deployment secrets, if hosted)

### Does not own

- Apple's software licence
- the macOS installer itself
- identity (Cerulean)

## Service map

| Component | Technology | Job |
| --- | --- | --- |
| macOS ISO Builder | Node.js / TypeScript | Build bootable macOS installer ISOs and DMGs from Apple's servers. |
| Identity | Cerulean Authentik | Sign-in and role claims, where the repo has a UI |
| Secrets | Cerulean Vault (KV v2) | Production credentials, referenced as `vault://` |
| Trust | Cerulean | DNS, TLS and the public hostname |
| Edge | NPM Edge | The public route in front of the service |

## In the ecosystem

- **Identity** comes from Cerulean Authentik; this repo holds no second account
  table and no password of its own.
- **Secrets** come from Cerulean Vault. `.env` is local only and is never
  committed; a `vault://` reference is resolved by the deployment.
- **Trust and edge** are Cerulean's and NPM Edge's. This repo does not write DNS
  records or call the NPM API directly.
- **Storage, billing and telephony** belong to ONYX, Magnate and Zeus
  respectively; macOS ISO Builder consumes them only where the boundaries above say
  so.

## See also

- [README](../README.md)
- [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack)
