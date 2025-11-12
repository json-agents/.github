# JSON Agents

<div align="center">

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/JSON-AGENTS/Standard)
[![License](https://img.shields.io/badge/license-Apache%202.0-green.svg)](https://github.com/JSON-AGENTS/Standard/blob/main/LICENSE)
[![Standard](https://img.shields.io/badge/standard-RFC%208259-orange.svg)](https://datatracker.ietf.org/doc/html/rfc8259)
[![Status](https://img.shields.io/badge/status-v1.0.0-success.svg)](https://github.com/JSON-AGENTS/Standard)

**A Universal JSON Specification for Portable AI Agents**

[📘 Specification](https://github.com/JSON-AGENTS/Standard/blob/main/json-agents.md) • [🤝 Contributing](https://github.com/JSON-AGENTS/Standard/blob/main/CONTRIBUTING.md)

</div>

---

## What is JSON Agents?

**JSON AGENTS** defines the **Portable Agent Manifest (PAM)** — a universal, JSON-native format for describing AI agents, their capabilities, tools, runtimes, and governance in a single, interoperable manifest.

It enables seamless agent portability across frameworks, platforms, and ecosystems without code translation.

### Why JSON Agents?

- **Framework Interoperability**: Convert between LangChain, OpenAI, AutoGen, MCP, and custom frameworks
- **Universal Standard**: One manifest format that works everywhere
- **Built-in Governance**: Security policies, sandboxing, and audit trails included
- **Multi-Agent Systems**: Orchestrate complex agent graphs with conditional routing
- **Production Ready**: Complete with URI scheme (`ajson://`) and policy expression language
- **Schema Validated**: JSON Schema 2020-12 ensures correctness

---

## Repository Structure

| Repository | Description | Status |
|------------|-------------|--------|
| [**Standard**](https://github.com/JSON-AGENTS/Standard) | Core PAM specification, schemas, and documentation | ✅ v1.0.0 |
| [**Validators**](https://github.com/JSON-AGENTS/Validators) | Reference validators (Python, Node.js, Go) | Coming Soon |
| [**Converters**](https://github.com/JSON-AGENTS/Converters) | Framework conversion tools (LangChain ↔ PAM, etc.) | Coming Soon |
| [**Registry**](https://github.com/JSON-AGENTS/Registry) | Public agent manifest registry service | Coming Soon |
| [**Examples**](https://github.com/JSON-AGENTS/Examples) | Real-world agent manifest examples | Coming Soon |

---

## 🚀 Quick Start

### Minimal Agent Manifest

```json
{
  "manifest_version": "1.0",
  "agent": {
    "id": "ajson://example.com/agents/hello",
    "name": "Hello Agent",
    "version": "1.0.0"
  },
  "capabilities": [
    {
      "id": "generation",
      "description": "Generate friendly greetings"
    }
  ]
}
```

### Complete Multi-Agent System

```json
{
  "manifest_version": "1.0",
  "profiles": ["core", "exec", "gov", "graph"],
  "agent": {
    "id": "ajson://example.com/agents/support-hub",
    "name": "Customer Support Hub"
  },
  "capabilities": [
    { "id": "routing" },
    { "id": "qa" },
    { "id": "classification" }
  ],
  "runtime": {
    "type": "node",
    "entrypoint": "dist/hub.js"
  },
  "security": {
    "sandbox": "container"
  },
  "policies": [
    {
      "id": "deny-external",
      "effect": "deny",
      "action": "tool.call",
      "where": "tool.endpoint !~ 'internal.corp'"
    }
  ],
  "graph": {
    "nodes": [
      { "id": "router", "ref": "ajson://example.com/agents/router" },
      { "id": "faq", "ref": "ajson://example.com/agents/faq" },
      { "id": "escalation", "ref": "ajson://example.com/agents/escalation" }
    ],
    "edges": [
      { "from": "router", "to": "faq", "condition": "message.intent == 'faq'" },
      { "from": "router", "to": "escalation", "condition": "message.priority > 8" }
    ]
  }
}
```

---

## Key Features

### Complete Capability Suite
7 standard capabilities with formal JSON schemas:
- **Summarization** — Condense content intelligently
- **Routing** — Direct messages by intent
- **Retrieval** — Query knowledge sources
- **QA** — Answer questions with context
- **Classification** — Categorize inputs
- **Extraction** — Extract structured data
- **Generation** — Create new content

### URI Scheme
Formal `ajson://` URI scheme (RFC 3986 compliant):
```
ajson://example.com/agents/router
→ https://example.com/.well-known/agents/router.agents.json
```

### Policy Expression Language
Declarative access control with rich operators:
```json
{
  "where": "tool.type == 'http' && tool.endpoint !~ 'external'"
}
```

### Modular Profiles
Progressive enhancement with 4 profiles:
- **Core** — Identity, capabilities, tools (required)
- **Exec** — Runtime metadata (optional)
- **Gov** — Security and policies (optional)
- **Graph** — Multi-agent orchestration (optional)

---

## Framework Support

| Framework | Import | Export | Status |
|-----------|:------:|:------:|--------|
| **LangChain** | ⚠️ | ⚠️ | Coming Soon |
| **OpenAI** | ⚠️ | ⚠️ | Coming Soon |
| **AutoGen** | ⚠️ | ⚠️ | Coming Soon |
| **Vercel AI SDK** | ⚠️ | ⚠️ | Coming Soon |
| **Anthropic** | ⚠️ | ⚠️ | Coming Soon |
| **MCP** | ⚠️ | ⚠️ | Coming Soon |
| **CrewAI** | ⚠️ | ⚠️ | Coming Soon |

---

## Documentation

| Resource | Description |
|----------|-------------|
| [**Specification**](https://github.com/JSON-AGENTS/Standard/blob/main/json-agents.md) | Complete PAM specification (888 lines) |
| [**Schema Reference**](https://github.com/JSON-AGENTS/Standard/tree/main/schema) | JSON Schema 2020-12 validators |
| [**Implementer's Guide**](https://github.com/JSON-AGENTS/Standard/blob/main/docs/implementers-guide.md) | How to parse, validate, and use manifests |
| [**Framework Mappings**](https://github.com/JSON-AGENTS/Standard/blob/main/docs/mapping-frameworks.md) | Convert to/from other agent formats |
| [**Extensions Guide**](https://github.com/JSON-AGENTS/Standard/blob/main/docs/extensions.md) | Create custom `x-*` extensions |
| [**Examples**](https://github.com/JSON-AGENTS/Standard/tree/main/examples) | Real-world manifest examples |

---

## Use Cases

- **Framework Migration**: Move agents between LangChain, OpenAI, AutoGen without rewriting
- **Agent Catalogs**: Build discoverable registries of reusable agents
- **Orchestration**: Define complex multi-agent workflows with conditional routing
- **Enterprise Governance**: Enforce security policies and maintain audit trails
- **Marketplaces**: Standardized format for distributing and monetizing agents
- **CI/CD Testing**: Schema-based validation for automated testing pipelines

---

### Contributing

We welcome contributions of all kinds:

- **Bug Reports**: Found an issue? Let us know!
- **Feature Proposals**: Have an idea? Open a discussion!
- **Documentation**: Help improve our docs
- **Tools**: Build validators, converters, or integrations
- **Framework Support**: Add mappings for new frameworks

See our [**Contributing Guide**](https://github.com/JSON-AGENTS/Standard/blob/main/CONTRIBUTING.md) for details.

**Code of Conduct**: This project follows the [Contributor Covenant 2.0](https://github.com/JSON-AGENTS/Standard/blob/main/CODE_OF_CONDUCT.md).

---

## Roadmap

### v1.0 (Current)
- ✅ Core, Exec, Gov, Graph profiles
- ✅ 7 capability schemas with formal validation
- ✅ URI scheme specification (`ajson://`)
- ✅ Policy expression language
- ✅ Framework mapping guide
- ✅ Complete documentation

### v1.1 (Q1 2026)
- Reference validator implementations (Python, Node.js, Go)
- Framework converter CLI tools
- Public registry service with API
- Additional capability schemas (dialogue, planning, reasoning)
- Community extension showcase

### v2.0 (Q3 2026)
- Real-time profile for streaming agents
- Evaluation profile for testing/benchmarking
- Enhanced policy expression functions
- Formal IETF/W3C standardization track
- Enterprise support packages

---

## Standards Compliance

JSON AGENTS is built on established foundations:

- ✅ [RFC 8259](https://datatracker.ietf.org/doc/html/rfc8259) — JSON Data Interchange Format
- ✅ [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986) — URI Generic Syntax
- ✅ [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119) — Requirement Levels
- ✅ [ECMA-404](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/) — JSON Data Interchange Syntax
- ✅ [ISO/IEC 21778:2017](https://www.iso.org/standard/71616.html) — JSON Standard
- ✅ [JSON Schema 2020-12](https://json-schema.org/draft/2020-12/json-schema-core.html) — Validation

---

## License

JSON AGENTS is released under the **Apache 2.0 License**.

See [LICENSE](https://github.com/JSON-Agents/Standard/blob/main/LICENSE) for details.

---

## Acknowledgments

JSON AGENTS draws inspiration from:
- JSON Schema and JSON-LD communities
- OpenAPI and AsyncAPI specifications
- Agent framework developers (LangChain, AutoGen, CrewAI)
- Model Context Protocol contributors
- [JsonResume.org](https://jsonresume.org)
- The broader open-source AI community

Special thanks to all contributors who have helped shape this standard.

---

<div align="center">

**⭐ Star us on GitHub to show your support!**

[Standard Repository](https://github.com/JSON-AGENTS/Standard) • [Documentation](https://github.com/JSON-AGENTS/Standard/blob/main/json-agents.md)

**Building the future of portable AI agents, together.**

</div>
