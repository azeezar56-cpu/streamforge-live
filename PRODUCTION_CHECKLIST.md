# Production hardening checklist

- [ ] Replace local SQLite with managed MongoDB/PostgreSQL or another managed persistent database; add migrations and backups.
- [ ] Implement real authentication, verified email, session rotation, MFA and tenant ownership checks before public exposure.
- [ ] Put API behind HTTPS and configure exact CORS origins.
- [ ] Store encryption master key in a managed KMS/secret manager and plan key rotation.
- [ ] Move FFmpeg to a dedicated persistent worker service; implement a durable queue and per-broadcast leases.
- [ ] Add media upload pipeline, malware/file validation, transcoding, object storage and signed URLs.
- [ ] Validate outbound RTMP host allowlists and defend against DNS rebinding/SSRF.
- [ ] Redact all endpoint credentials from process arguments, logs and crash reports; consider secret injection through a protected local pipe where supported.
- [ ] Add platform OAuth, official API review, eligibility checks, rate limits and token revocation.
- [ ] Add metrics, alerts, structured logs, resource quotas, retention policies and incident runbooks.
- [ ] Run load, reconnect, crash recovery, network loss, disk full and destination rejection tests.
- [ ] Replace Android WebView local URL with production HTTPS domain and implement native secure session storage.
- [ ] Remove `usesCleartextTraffic=true` for production and enforce HTTPS.
- [ ] Perform a security review before storing real user stream keys.
