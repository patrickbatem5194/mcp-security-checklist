# 🔌 API Session Security

**Audience:** Platform and infrastructure teams
**Risk level if skipped:** High

---

## Why It Matters

MCP servers receive sessions from AI agents — but unlike a human user clicking around a UI, agents can issue hundreds of requests per second, chain tools in unexpected sequences, and operate outside normal business hours. Traditional API security assumes a human is on the other end. Agentic sessions require a different threat model.

---

## Checklist

### Session Management

- [ ] **Assign a unique session ID to every agent interaction** — this is essential for tracing multi-step tool chains.
- [ ] **Enforce session timeouts** — agent sessions should not remain open indefinitely.
- [ ] **Invalidate sessions on anomalous behavior** — excessive tool calls, unexpected tool sequences, or calls outside expected operational windows.
- [ ] **Do not allow session tokens to be passed via query parameters** — use headers (Authorization, X-Session-Token) instead.
- [ ] **Bind sessions to a specific agent identity**, not just a valid token — token reuse across different agent contexts is a risk.

### Rate Limiting

- [ ] **Apply rate limits per session and per tool** — not just at the server level.
- [ ] **Set separate limits for read vs. write/execute tools** — write operations should have stricter throttling.
- [ ] **Alert on sustained high-frequency tool calls** — this is unusual for legitimate agent behavior and may indicate a loop or abuse.
- [ ] **Implement exponential backoff enforcement** — penalize repeated failures rather than allowing infinite retries.

### Request Integrity

- [ ] **Validate that requests conform to expected patterns for the agent's stated task** — an agent tasked with summarizing documents shouldn't be calling email-send tools.
- [ ] **Log the full request context for every tool call**: session ID, timestamp, tool name, input summary (not raw inputs if sensitive), and response status.
- [ ] **Reject requests with missing or malformed session context** — don't silently accept them.
- [ ] **Consider signing requests from your agent orchestrator** to detect tampering in transit.

---

## Agentic vs. Human Session Differences

| Property | Human Session | Agent Session |
|----------|--------------|---------------|
| Request velocity | Low (human-paced) | Potentially very high |
| Session duration | Minutes to hours | Can be indefinite |
| Tool chain predictability | N/A | Should be bounded by task |
| Off-hours activity | Unusual | Normal for automated agents |
| Error tolerance | Human catches errors | Errors can propagate silently |

Design your session security with these differences in mind.

---

## References

- [OWASP API Security — API4: Lack of Resources & Rate Limiting](https://owasp.org/www-project-api-security/)
- [OWASP API Security — API2: Broken Authentication](https://owasp.org/www-project-api-security/)

---

*[← Tool Exposure](03-tool-exposure.md) | [Back to README](../README.md) | [Next: Monitoring →](05-monitoring.md)*
