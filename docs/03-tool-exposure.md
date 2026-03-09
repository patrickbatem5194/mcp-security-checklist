# 🧰 Tool & Resource Exposure

**Audience:** Engineers and architects designing MCP servers
**Risk level if skipped:** High

---

## Why It Matters

Every tool you expose is a capability an attacker can attempt to abuse. The more tools an agent has access to, the larger the blast radius if something goes wrong — whether due to a compromised agent, a prompt injection, or a misconfigured permission. Minimizing and controlling tool exposure is one of the most effective risk reduction strategies available.

---

## Checklist

### Tool Inventory

- [ ] **Maintain a formal inventory of all exposed tools** — name, purpose, permissions required, and owner.
- [ ] **Review the tool inventory before every deployment** — remove tools that are no longer needed.
- [ ] **Document what each tool can access** — files, databases, external APIs, network resources.
- [ ] **Flag high-risk tools explicitly** — tools that can send data externally, modify files, or trigger financial transactions require additional scrutiny.

### Blast Radius Reduction

- [ ] **Expose only the tools an agent actually needs** for its current task — not every tool it might ever use.
- [ ] **Use separate MCP server instances for different agent roles** — don't serve admin tools and read-only tools from the same endpoint.
- [ ] **Apply resource-level scoping** — a tool that reads from a database should be scoped to specific tables or schemas, not the entire database.
- [ ] **Disable or remove tools in production that were only needed during development.**
- [ ] **Consider "tool budget" per session** — agents that suddenly invoke a much wider range of tools than normal may indicate compromise or injection.

### External Resource Access

- [ ] **Audit all external APIs your MCP tools call** — each one is a potential data exfiltration path.
- [ ] **Apply egress filtering** — MCP servers should not be able to make arbitrary outbound connections.
- [ ] **Require allow-listing for any tool that fetches external content** (URLs, files from arbitrary paths, etc.).
- [ ] **Do not allow tools to make outbound calls to addresses derived from agent inputs** without strict validation.

---

## Common Mistakes

| Mistake | Risk |
|--------|------|
| Exposing all tools to all agents | Compromised agent gains maximum capability |
| Dev tools left enabled in production | Debugging tools often carry elevated privileges |
| Tools that can write to arbitrary file paths | Path traversal → full filesystem access |
| MCP server with unrestricted outbound networking | Exfiltration via tool-initiated external calls |

---

## Think in Terms of "What Could Go Wrong"

For each tool, ask:
1. **If this tool is called with adversarial inputs, what's the worst outcome?**
2. **If an agent is compromised and calls this tool repeatedly, what damage could it do?**
3. **Does this tool need to exist in production, or only during development?**

---

## References

- [OWASP LLM Top 10 — LLM06: Sensitive Information Disclosure](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [Principle of Least Privilege — NIST](https://csrc.nist.gov/glossary/term/least_privilege)

---

*[← Input Validation](02-input-validation.md) | [Back to README](../README.md) | [Next: API Session Security →](04-api-session.md)*
