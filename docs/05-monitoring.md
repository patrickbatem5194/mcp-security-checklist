# 📡 Monitoring & Observability

**Audience:** Security operations and platform teams
**Risk level if skipped:** High

---

## Why It Matters

You can't detect what you don't log. MCP deployments introduce a new category of activity — autonomous tool invocations — that most existing SIEM and observability pipelines weren't built for. Establishing baseline logging and alerting now makes incident response dramatically faster when something goes wrong.

---

## Checklist

### What to Log

- [ ] **Every tool invocation**: session ID, agent identity, tool name, timestamp, success/failure.
- [ ] **Input metadata** (not raw sensitive content): input length, schema match/fail, any validation errors triggered.
- [ ] **Tool chain sequences**: the ordered list of tools called within a session — unusual chains are a key detection signal.
- [ ] **Latency and response size per tool call** — sudden spikes can indicate abuse or malfunction.
- [ ] **Authentication events**: token issuance, expiry, rejection, rotation.
- [ ] **Rate limit hits**: which sessions hit limits, how often, and on which tools.
- [ ] **Session lifecycle events**: creation, timeout, explicit termination, and anomalous termination.

### What to Alert On

- [ ] **Sudden spike in tool call volume from a single session** — could indicate a runaway loop or abuse.
- [ ] **First-seen tool invocations** — a tool that has never been called before being invoked in production.
- [ ] **Unusual tool chain sequences** — especially when high-risk tools (file write, external API call) follow low-risk tools (read, search) in a single session.
- [ ] **Off-hours activity from agents with no expected off-hours use case.**
- [ ] **Repeated authentication failures** from the same source.
- [ ] **Calls to tools outside the agent's stated purpose or task scope** (if you track task context).

### Observability Infrastructure

- [ ] **Centralize MCP logs** into your existing SIEM or log aggregation platform — don't leave them siloed on the MCP server.
- [ ] **Retain logs for a minimum of 90 days** — agentic attack chains can take time to fully manifest.
- [ ] **Ensure logs are tamper-evident** — if your MCP server is compromised, log integrity matters.
- [ ] **Build a baseline of normal behavior** for each deployed agent before relying on anomaly alerts — without a baseline, everything looks suspicious.
- [ ] **Test your alerting pipeline** — confirm that a real anomalous event would actually page someone.

---

## Useful Baseline Metrics to Track

| Metric | Why It Matters |
|--------|---------------|
| Average tools called per session | Baseline for detecting session-level anomalies |
| Most common tool chains | Helps identify unexpected sequences |
| Tool call failure rate | Elevated failures may indicate fuzzing |
| P99 latency per tool | Useful for detecting resource exhaustion |
| Sessions per agent identity per hour | Useful for detecting token abuse |

---

## References

- [OWASP LLM Top 10 — LLM08: Excessive Agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [NIST Cybersecurity Framework — Detect Function](https://www.nist.gov/cyberframework)

---

*[← API Sessions](04-api-session.md) | [Back to README](../README.md) | [Next: Network & Infrastructure →](06-network.md)*
