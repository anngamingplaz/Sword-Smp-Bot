# Security and malware audit

## Result

The repository was reviewed for common malware indicators: shell execution, child-process spawning, obfuscated payloads, suspicious downloads, credential exfiltration, and hidden remote-control code. No standalone virus or destructive payload was found in the tracked source files reviewed.

## Critical security issue fixed

The public repository contained a server authentication password in `settings.json`. It has been removed and auto-auth has been disabled. **Rotate that password immediately** because deleting it from the latest commit does not remove it from Git history.

## Remote-control risk

The dashboard previously exposed `/start`, `/stop`, and `/command` without authentication. If the hosting provider exposes the dashboard publicly, anyone who discovers the URL could send Minecraft chat/commands. Do not expose this service publicly until authentication or private networking is added.

Recommended deployment controls:

1. Set the service to private or restrict ingress with an access token/reverse proxy.
2. Never grant the bot operator privileges.
3. Keep `try-creative` disabled.
4. Use a fresh server password and rotate any Discord webhook that was ever committed.
5. Review Git history and hosting logs for unauthorized requests.
6. Run `npm audit` before deployment and keep the lockfile committed.

This audit cannot prove that a compromised hosting environment or untracked file is clean; inspect the deployed machine separately if you suspect an active compromise.
