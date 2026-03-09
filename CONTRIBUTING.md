# Contributing to MCP Security Checklist

First off — thank you. This checklist improves when practitioners with real-world MCP deployment experience share what they've learned.

---

## What We're Looking For

### ✅ Great contributions

- **New checklist items** based on real-world misconfigurations or attack patterns you've observed
- **Corrections** to existing items — if something is wrong or misleading, please tell us
- **New checklist categories** — we may be missing coverage on areas like supply chain, CI/CD pipeline security, or multi-agent architectures
- **References** — links to relevant papers, CVEs, OWASP items, or standards we should cite
- **Machine-readable improvements** — fixes or extensions to `checklist.json` or `checklist.yaml`

### ❌ Out of scope

- Vendor-specific tooling recommendations (this checklist stays vendor-neutral)
- Model training or fine-tuning security (outside the scope of MCP deployment)
- General AI ethics or governance topics

---

## How to Contribute

### Option 1: Open an Issue

The fastest way to suggest a change. Use one of the issue templates:

- **New checklist item** — suggest a control we're missing
- **Correction** — flag something that's wrong or outdated
- **New category** — propose a new section

### Option 2: Submit a Pull Request

1. Fork the repository
2. Create a branch: `git checkout -b add/your-contribution`
3. Make your changes
4. Submit a PR with a clear description of what you changed and why

---

## Checklist Item Format

When proposing a new checklist item, please follow this format:

```markdown
- [ ] **[Short, imperative description of the control]**  
  _Why it matters: [One to two sentences explaining the risk it mitigates]_
```

For the machine-readable formats, follow the existing schema in `checklist.json` / `checklist.yaml`.

---

## Quality Bar

We apply a simple test to every item:

> **"Would a security engineer or platform team lead look at this and immediately understand what to do and why it matters?"**

Items that are too vague ("implement security best practices"), too obvious ("use HTTPS"), or that can't be acted on independently are unlikely to be merged.

---

## Code of Conduct

Be direct, be constructive, be kind. We're all trying to make agentic AI deployments safer.

---

## Questions?

Open an issue or reach out via [helixar.ai](https://helixar.ai).

*Maintained by the [Helixar](https://helixar.ai) security research team.*
