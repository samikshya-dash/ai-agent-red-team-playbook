# Tooling: manual, PyRIT and the Foundry AI Red Teaming Agent

[← Back to the playbook](../README.md)

I use three approaches together. Each finds things the others miss.

| Approach | Best for | Limits |
|---|---|---|
| **Manual testing** | Findings that depend on what *this* agent can reach and do: cross-user access, tool misuse, indirect injection through its real data sources | Slow; coverage depends on the tester |
| **PyRIT** (Microsoft's open-source Python Risk Identification Tool) | Breadth and repeatability: many prompts, many converters, scored automatically, re-run on every release | Needs test cases written for the agent's context; automated scoring needs spot checks |
| **Microsoft Foundry AI Red Teaming Agent** | Scanning models and agents in Foundry against safety risk categories, with a scorecard | Works on what Foundry can reach; the categories are fixed |

## How they fit the method

| Step in this playbook | Manual | PyRIT | Foundry AI Red Teaming Agent |
|---|---|---|---|
| Map the agent | Read the configuration; ask the six questions | — | — |
| Probe | Hand-written prompts and conversations | Datasets of objectives sent through converters to a target | Attack strategies run against a risk category |
| Disguise the request | By hand | Converters | Attack strategies such as Base64, ROT13, Leetspeak, CharacterSpace, Jailbreak, Indirect Jailbreak, Multi Turn and Crescendo |
| Score | Canary or marker observed | Scorers | Evaluators |
| Measure | Findings by severity | Attack success rate | Attack success rate (ASR) on a scorecard |

## Foundry AI Red Teaming Agent risk categories

At the time of writing, the service lists these categories. The last three apply to agents only.

| Model and agent | Agent only |
|---|---|
| Hateful and Unfair Content · Sexual Content · Violent Content · Self-Harm-Related Content · Protected Materials · Code Vulnerability · Ungrounded Attributes | Prohibited Actions · Sensitive Data Leakage · Task Adherence |

The three agent-only categories line up with this playbook's excessive permissions, data leakage and unsafe content tests. Check [Microsoft's documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ai-red-teaming-agent) for the current list; it is updated often.

## Where automated tools stop

Automated scans are good at "can the model be made to say X". They are weaker at "can user A make the agent do something to user B's data", because that depends on the agent's tools, identities and data, which the scanner doesn't know. Those are usually the Critical findings, and they need the threat model and a person.

**My order of work:** map the agent, test the high-impact chains by hand, then use automation for breadth and for regression on every release.

## Copilot Studio agents

For agents built in Copilot Studio, the configuration review carries much of the weight: authentication setting, who the agent is shared with, which connectors and tools it holds and whose credentials they use, which knowledge sources it reads, and whether generative orchestration lets it choose tools freely. The test pane is useful for watching which topics and tools a prompt triggers.

## Logs to check after testing

A test isn't finished until you have looked from the defender's side: did the platform log the attempt, did a detection fire, would anyone have noticed? Queries for that are in [ai-agent-exposure-hunting](https://github.com/samikshya-dash/ai-agent-exposure-hunting).

[← Fixes](06-fixes.md) · [Back to the playbook](../README.md)
