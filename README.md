# Finance skills

Four AI skills that split an investment committee into separate roles: an analyst who builds the case, a risk officer who attacks it, a macro analyst who sets the regime, and a portfolio manager who decides how much capital it gets.

They work with any capable AI model. Each skill is a plain Markdown prompt (`SKILL.md`) in the open Agent Skills format, so nothing in them is tied to one vendor.

## What they do

| Skill | Role | What it returns |
|---|---|---|
| [buy-side-equity-analyst](skills/buy-side-equity-analyst) | Builds the case | Fundamental research on one company: business, moat, financial quality, management, valuation, bear case, catalysts, bull/base/bear scenarios, a confidence score and a position suitability call |
| [chief-risk-officer](skills/chief-risk-officer) | Attacks it | Assumes the thesis is wrong: the assumptions underneath it, three failure scenarios, a worst case with drawdown, hidden and portfolio-level risks, a risk rating and an approve-to-reject action |
| [macro-analyst](skills/macro-analyst) | Sets the regime | Classifies the economy into one of six regimes, reads rates, inflation, growth, liquidity, credit and policy, and turns that into sector and factor positioning with scenario probabilities |
| [portfolio-manager](skills/portfolio-manager) | Sizes the position | Takes the other three outputs and your holdings and returns a position size, its effect on portfolio risk and correlation, the opportunity cost, and a verdict from add to exit |

## How they work together

One model arguing both sides of a trade tends to hedge. Giving each argument its own prompt makes each one get made properly.

| Order | Skill | Input |
|---|---|---|
| Any time | macro-analyst | Current rate, inflation and growth data. It doesn't pick stocks. |
| 1 | buy-side-equity-analyst | A company name, plus filings or financials if you have them |
| 2 | chief-risk-officer | The analyst's write-up |
| 3 | portfolio-manager | All of the above and your current holdings |

Each skill also works alone. The risk officer is most useful on ideas you already like.

## Requirements

| Need | Why |
|---|---|
| A capable AI model | The skills are prompts; there is no code |
| Current data: a model with web search, or filings, prices and macro figures you paste in | A model's training data has a cutoff. Without fresh numbers it reasons from stale ones, which the skills can't catch on their own. |
| Your holdings, for the portfolio manager | Its correlation and concentration checks need something to work against |

No API keys and no packages to install.

## Install

| Where you run it | How |
|---|---|
| An agent that reads skills folders (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot, Cursor and the others listed at [agentskills.io](https://agentskills.io)) | Clone the repo and copy the skill folders into the agent's skills folder. Each agent documents its own location. |
| A chat assistant without skills (ChatGPT, Gemini, Claude.ai, a local model) | Paste a skill's `SKILL.md` (below the `---` header) into custom instructions, a project, a Gem, or the first message. One conversation or project per role keeps the roles apart. |

With Claude Code as the example agent:

```bash
git clone https://github.com/Vidwaansinghania/Finance-Skills.git
cp -r Finance-Skills/skills/* ~/.claude/skills/
```

Swap `~/.claude/skills/` for your agent's skills folder. To take one skill only, copy just that folder.

## Other AI skills

Each of these has its own repo:

| Repo | What it does |
|---|---|
| [Lecture-Notes-Builder](https://github.com/Vidwaansinghania/Lecture-Notes-Builder) | Merges a lecture transcript and slides into one exam-ready Obsidian note |
| [Timetable-to-ICS](https://github.com/Vidwaansinghania/Timetable-to-ICS) | Turns a timetable into an .ics file and checks every event against the source |
| [Vault-Health-Check](https://github.com/Vidwaansinghania/Vault-Health-Check) | Audits an Obsidian vault for orphans and broken links and fixes the safe ones |
| [PDF-to-Profile-Note](https://github.com/Vidwaansinghania/PDF-to-Profile-Note) | Turns a personality report or study guide PDF into a page-cited Profile note |
| [Project-README-Publisher](https://github.com/Vidwaansinghania/Project-README-Publisher) | Writes tab-style GitHub docs from project notes and opens a pull request |

The multi-agent equity research pipeline is a larger project with its own repo: [Multi-Agent-Equity-Research](https://github.com/Vidwaansinghania/Multi-Agent-Equity-Research).

## Licence

MIT. See [LICENSE](LICENSE).

## Disclaimer

These are prompts, not an investment adviser. Output is generated text and can be wrong, stale or confidently mistaken about facts. Nothing they produce is investment advice. Verify every number against primary sources before acting on any of it.
