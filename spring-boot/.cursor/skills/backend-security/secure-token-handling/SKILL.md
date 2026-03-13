---
name: secure-token-handling
description: Handles JWT generation, validation, storage, and refresh securely. Use when implementing or reviewing JWT-based auth and token lifecycle.
---

# Secure Token Handling

## When to Apply

Use when the user implements or reviews JWT issuance, validation, refresh, or storage (Java/Spring Boot, jjwt or Spring Security OAuth2 Resource Server).

## Conventions (JWT)

- **Generation**: Sign JWTs with a strong algorithm (e.g. RS256 or HS256 with a long secret). Set short expiry for access tokens (e.g. 15–60 min). Put minimal claims (sub, roles, exp, iat); avoid sensitive data in payload.
- **Validation**: Verify signature, expiry (`exp`), and issuer (`iss`) if used. Reject malformed or expired tokens; return 401. Use a single source for signing key/secret (config or key store).
- **Storage**: Server-side: do not store tokens in logs or in session storage that is logged. Client-side guidance: recommend httpOnly cookies for web if applicable, or secure storage; avoid localStorage for tokens when XSS is a concern.
- **Refresh**: Use opaque refresh tokens stored server-side (e.g. in DB) with expiry and revocation. Issue new access (and optionally refresh) token after validating refresh token; rotate or revoke refresh token on use if required by policy.
- **Transmission**: Use HTTPS only. Prefer `Authorization: Bearer <token>` for APIs. Do not put tokens in URL query params.

## Output

- Example of building and signing a JWT (e.g. jjwt `Jwts.builder()`) and validating in a filter or resolver.
- Config placeholders for secret/key path and expiry.
- Short do/don’t list: short expiry, verify signature, no secrets in payload, HTTPS, secure storage.
