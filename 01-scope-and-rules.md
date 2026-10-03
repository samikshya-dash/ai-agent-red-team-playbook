# 1. Scope and rules of engagement

[← Back to the playbook](../README.md)

A red team exercise on an AI agent is authorised testing against a live system that can read data and take actions. Agree the boundaries in writing before sending the first prompt.

## What to agree before you start

| Question | Why it matters |
|---|---|
| **Which agent, which version, which environment?** | A test copy is safest. If production is the only option, restrict tests to test accounts and reversible actions |
| **Who owns the agent and who signs off the test?** | Findings need an owner who can fix them. No named owner, no test |
| **What can the agent reach?** | Knowledge sources, connectors, tools, MCP servers, identities it acts as. This list *is* the attack surface |
| **Which actions are out of bounds?** | Sending real email, changing real records, anything that costs money or touches real customers |
| **Which test accounts and data?** | At least two test users with different access, each holding marker data you can recognise in a leak |
| **What counts as a finding?** | Agree the severity scale first ([page 4](04-severity.md)), so results aren't argued after the fact |
| **How are transcripts stored?** | Test conversations can contain leaked data. Store them like any other security evidence |
| **Who do you call if something real breaks?** | Name a contact and a stop condition |

## Rules I work to

1. **Written authorisation first.** Named agent, named tester, dates, environment.
2. **Test accounts and planted data only.** Use canaries: unique marker strings placed in the instructions, the knowledge base and each test user's data. A leak is then a yes-or-no observation.
3. **Stop at proof.** One clear demonstration that an action or leak is possible is enough. Don't expand the impact to make a point.
4. **No real harm for the sake of a test.** Unsafe-content tests use harmless markers and out-of-scope requests. The question is whether the guardrail holds, and a harmless request answers it.
5. **Report sensitive findings privately,** to the owner, before anyone else.
6. **Leave it as you found it.** Remove canaries, test documents and test accounts afterwards.

## Before-you-start checklist

- [ ] Authorisation signed, with dates and environment
- [ ] Agent inventory: instructions, knowledge sources, tools, connectors, identities, channels
- [ ] Two or more test users with distinct marker data
- [ ] Canary planted in a test copy of the instructions
- [ ] Out-of-bounds actions listed, and tools pointed at test systems where possible
- [ ] Severity scale agreed
- [ ] Logging confirmed on, so the defenders' view can be checked afterwards
- [ ] Emergency contact and stop condition agreed

A fill-in version is in [`templates/rules-of-engagement.md`](../templates/rules-of-engagement.md).

[Next: Threat model →](02-threat-model.md)
