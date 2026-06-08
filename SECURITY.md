# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in WhitelistBot, please do NOT open a public issue.

Instead, report it privately to the project maintainer:

- **Discord**: https://discord.gg/zyqsPMnXpU

Please include:
- A clear description of the vulnerability
- Steps to reproduce (if possible)
- Potential impact

## What to Expect

- You'll receive an acknowledgment within 48 hours
- A fix will be prioritized based on severity
- You'll be credited (if desired) when the fix is published

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.x     | ✅ Yes |

## Security Best Practices

### For Server Admins

1. **Change the default API key** in `plugins/WhitelistBot/config.yml` before pairing
2. **Keep the API key secret** — it authorizes whitelist changes on your server
3. **Use a firewall** to restrict port 25252 to your Discord bot's IP if possible
4. **Enable anti-alt** in config if you want to prevent multiple accounts per IP
5. **Set an unlink cooldown** to prevent abuse (default: 1 week)
6. **Restrict whitelist access** by assigning a role via `>setup role:@role`

### Known Security Properties

| Property | Status |
|----------|--------|
| API key transmitted in cleartext | ⚠️ Plain HTTP (no TLS) — use a VPN or local network for production |
| Pairing codes are one-time | ✅ Expire after 5 minutes or first use |
| API key comparison is constant-time | ✅ Prevents timing side-channel attacks |
| SQL injection | ✅ Mitigated by parameterized queries (better-sqlite3) |
| SSRF | ✅ Private IP ranges blocked by Discord bot |
| DoS via HTTP server | ✅ Mitigated by bounded thread pool (max 10 threads) |
| Disk I/O on player join | ✅ Debounced to once per 5 seconds |
