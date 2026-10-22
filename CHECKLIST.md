# AI Agent Semantic Layer Integration Checklist

## Pre-Deployment Gates

1. **Document every table and column the agent may access, including sensitivity classification and owning team.**
   *Rationale: Agents cannot infer data sensitivity or ownership from schema names alone.*

2. **Define business-vocabulary mappings for every concept the agent will be asked about (e.g., "revenue," "active customer").**
   *Rationale: Raw schemas use implementation names; agents need a common business vocabulary to select the correct tables.*

3. **Specify which roles or individuals are authorized to see each semantic entity, and enforce this at query time, not in metadata alone.**
   *Rationale: Describing authorization in metadata does not prevent the agent from returning restricted data to unauthorized users.*

4. **Implement minimum-necessary permission scoping: the agent's credentials must not exceed what any single user querying through it is allowed to see.**
   *Rationale: Agents should not operate with union permissions that let them bypass row-level or column-level security.*

5. **Time-bound agent access: set expiration on credentials and require re-authorization after a defined period.**
   *Rationale: Persistent credentials enable long-lived exposure if an agent is compromised or misconfigured.*

6. **Log every query the agent generates, including the requesting user, timestamp, semantic intent, and SQL executed.**
   *Rationale: Without logs, you cannot diagnose over-permissioned queries or trace data exfiltration after the fact.*

7. **Test the agent against a realistic set of ambiguous or adversarial questions to confirm it does not return unauthorized data.**
   *Rationale: Benign test queries will not surface the agent's behavior when a user deliberately or accidentally requests restricted information.*

8. **Establish a rollback procedure to revoke agent access and revert to manual query workflows within one business day.**
   *Rationale: If the agent begins returning incorrect or unauthorized results, you must be able to disable it without disrupting core operations.*

## Recommended Controls

9. **Validate every agent-generated query against a known-good query catalog or pattern library before execution.**
   *Rationale: Structural validation can catch malformed or suspicious queries that bypass semantic-layer guardrails.*

10. **Filter agent output to remove any column not explicitly declared in the semantic layer, even if the query technically succeeded.**
    *Rationale: Agents may select columns outside the intended business vocabulary if schema introspection is allowed.*

11. **Rate-limit agent queries per user and per session to detect runaway or exfiltration-style access patterns.**
    *Rationale: High-frequency queries from a single session may indicate automated data extraction rather than interactive analysis.*

12. **Review agent query logs weekly with a data steward to identify unintended access patterns or business-vocabulary gaps.**
    *Rationale: Emergent misuse or confusion often appears in aggregate patterns, not in any single query.*

13. **Document every business metric or KPI the agent is expected to surface, and validate that its query logic matches the canonical definition used by BI tools.**
    *Rationale: Divergence between agent-reported metrics and dashboard metrics erodes trust and leads to conflicting decisions.*

14. **Require governance review before adding new tables or columns to the agent's semantic layer.**
    *Rationale: Expanding the vocabulary also expands the attack surface and the risk of accidental disclosure.*

15. **Test the agent's behavior when a user asks a question that spans multiple permission boundaries (e.g., asking for customer revenue when the user can see customers but not revenue).**
    *Rationale: Cross-boundary queries are a common failure mode; the agent must deny the request or redact the restricted portion, not silently omit it.*

## Incident Response

16. **Define an incident-response playbook for scenarios where the agent returns data the requesting user should not have seen.**
    *Rationale: Detection is only useful if your team knows who to notify, which logs to pull, and how to contain the exposure.*

17. **Maintain a contact list of data owners for every table in the semantic layer so you can notify them if their data is queried in an anomalous pattern.**
    *Rationale: Data owners are often the first to recognize when usage does not match legitimate business activity.*