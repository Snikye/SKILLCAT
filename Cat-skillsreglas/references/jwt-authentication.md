# JWT Asymmetric Authentication

## RS256 Requirement

For API-exposed JWT authentication and authorization, prefer asymmetric RSA signing with a minimum 2048-bit key and the RS256 algorithm.

Do not introduce HS256 or shared-secret JWT signing for new API authentication flows unless the existing system has an explicit approved exception from the user or project security owner.

## Key Custody

- Private keys are used only by the issuer/signing component.
- Store private keys in secure encrypted custody such as Azure Key Vault, AWS KMS, HSM-backed storage, or the project-approved equivalent.
- Consumer services should verify tokens with public keys only.
- Do not commit private keys, certificates, development secrets, or fallback signing keys.

## Token Validation

Validate the trust chain and standard claims on each request:

- `iss`
- `aud`
- `exp`
- `nbf`
- `iat`
- `sub`
- `jti`

Use strict issuer, audience, lifetime, algorithm, and signing-key validation. Avoid accepting `alg=none`, algorithm downgrades, missing expiration, or ambiguous issuer/audience settings.

## Operational Notes

- Design for key rotation through key identifiers when the platform supports it.
- Keep token lifetimes bounded.
- Avoid logging full JWTs or sensitive claims.
- Treat authorization policy as server-side enforcement, never frontend-only behavior.
