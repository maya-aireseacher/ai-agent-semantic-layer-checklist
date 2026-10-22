# AI Agent Semantic Layer Integration Checklist

A structured checklist for teams deploying AI agents that query enterprise data. This checklist addresses the gap between an agent's ability to write SQL and its understanding of what the data means, who can see it, and which tables actually answer the business question.

## Who this is for

Data platform teams, AI engineering leads, and governance officers preparing to deploy AI agents with database access. If your agent can technically query your schema but you're unsure whether it will surface the right data to the right people, this checklist is for you.

## How to use it

Work through CHECKLIST.md with your cross-functional team before granting an agent access to production data. Each item includes a one-line rationale. Use checklist.csv to track ownership and completion. Treat items 1-8 as mandatory gates; items 9-15 are strongly recommended for production deployments.

## What it covers

- Schema and metadata documentation
- Business vocabulary mapping
- Permission scoping and time-bounding
- Query validation and output filtering
- Audit logging and incident response
- Governance review and rollback procedures

## Limitations

This checklist assumes you are implementing a semantic layer (such as dbt metrics, Looker LookML, or a custom business vocabulary service) between your agent and raw schemas. It does not cover general LLM security, prompt injection defenses unrelated to data access, or the decision of whether to deploy an agent in the first place. It is not a substitute for enterprise security review or legal counsel on data handling obligations.

## Contributing

This checklist reflects known failure modes as of early 2025. If your team encounters a gap not covered here, open an issue describing the scenario and the control you implemented.

## Further reading

- [Why Semantic Layers Are Becoming the Backbone of Enterprise AI Agents](https://www.aibmag.com/trending-ai-enterprise-solutions/why-semantic-layers-are-becoming-the-backbone-of-enterprise-ai-agents/)
- [Can LLMs Help You at Work? A Sandbox for Evaluating LLM Agents in Enterprise Environments (aclanthology.org)](https://aclanthology.org/2025.emnlp-main.466/)
- [The state of AI 2025 (mckinsey.com)](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai-2025)
- [Headless vs native semantic layer the architectural key to unlocking 90 text (venturebeat.com)](https://venturebeat.com/infrastructure/headless-vs-native-semantic-layer-the-architectural-key-to-unlocking-90-text)
- [how-microsoft-defends-against-indirect-prompt-injection-attacks (microsoft.com)](https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks)
- [OWASP Gen AI Incident & Exploit Round-up, Q2'25 (genai.owasp.org)](https://genai.owasp.org/2025/07/14/owasp-gen-ai-incident-exploit-round-up-q225/)
- [GitHub - RelationalAI/xlang-spider2: [ICLR 2025 Oral] Spider 2.0: Evaluating Language Models on Real-World Enterprise Te (github.com)](https://github.com/RelationalAI/xlang-spider2)
- [Heisenberg Institute: research and publications](https://www.heisenberg.institute)