---
title: Well-Known URIs
published: 2025-04-22
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Web Information Gathering
draft: false
---

## **Well-Known URIs — Summary**

### What is `.well-known`?

Defined in **RFC 8615**, the `.well-known/` directory is a **standardized location** on a web server where applications, browsers, and tools can retrieve important **metadata and configuration files**.

Typical Path:  
```
https://example.com/.well-known/
```

Maintained by **IANA**, each URI has a defined structure and purpose to support standardized discovery mechanisms.

---

## Why It's Useful for Recon

In **web reconnaissance**, `.well-known` URIs can:
- Expose security-relevant endpoints
- Reveal authentication and configuration details
- Aid in **endpoint mapping** and **metadata analysis**

---

## Common Well-Known URIs

| URI Suffix                  | Purpose                                                | Status       | Reference |
|----------------------------|--------------------------------------------------------|--------------|-----------|
| `security.txt`             | Contact info for reporting security vulnerabilities    | Permanent    | [RFC 9116](https://datatracker.ietf.org/doc/html/rfc9116) |
| `change-password`          | Redirects users to a change password page              | Provisional  | [W3C Spec](https://w3c.github.io/webappsec-change-password-url/#the-change-password-well-known-uri) |
| `openid-configuration`     | OpenID Connect metadata for authentication             | Permanent    | [Spec](http://openid.net/specs/openid-connect-discovery-1_0.html) |
| `assetlinks.json`          | Verify app-domain associations (e.g. Android apps)     | Permanent    | [Google Spec](https://github.com/google/digitalassetlinks) |
| `mta-sts.txt`              | Email security policy for SMTP MTA-STS                 | Permanent    | [RFC 8461](https://datatracker.ietf.org/doc/html/rfc8461) |

---

## Recon Example: `openid-configuration`

### Endpoint:
```
https://example.com/.well-known/openid-configuration
```

Returns metadata like:
```json
{
  "issuer": "https://example.com",
  "authorization_endpoint": "https://example.com/oauth2/auth",
  "token_endpoint": "https://example.com/oauth2/token",
  "userinfo_endpoint": "https://example.com/oauth2/userinfo",
  "jwks_uri": "https://example.com/oauth2/jwks",
  "response_types_supported": ["code", "token", "id_token"],
  "scopes_supported": ["openid", "profile", "email"]
}
```

### What You Can Discover:
- `authorization_endpoint`: Login URL
- `token_endpoint`: Where tokens are issued
- `jwks_uri`: Location of public signing keys
- Supported `algorithms`, `scopes`, and `response types`

---

## Recon Cheat Sheet

### Check for Common Well-Known Files
```bash
curl https://target.com/.well-known/security.txt
curl https://target.com/.well-known/openid-configuration
curl https://target.com/.well-known/change-password
```

### Enumerate All .well-known URIs from IANA
Visit: [IANA Well-Known URI Registry](https://www.iana.org/assignments/well-known-uris/well-known-uris.xhtml)

---

## Key Takeaways

- `.well-known/` is a **goldmine** for **metadata, security policies, and config info**.
- Especially useful in **auth-related discovery** and **target profiling**.
- **Always check** for unexpected `.well-known` entries in recon!



