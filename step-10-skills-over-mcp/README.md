# Step 10: Skills over MCP

> 🚧 **Under development.** This step is being written. The plan below shows what it will cover, and the code and instructions are coming soon.

Ship *know-how* along with tools. Skills over MCP lets a server provide packaged instructions (skills) that teach the model how to use the server's tools well for specific tasks.

> **Note:** Client support for this extension is still rolling out. Check the [client support matrix](https://modelcontextprotocol.io/extensions/client-matrix) for current Claude and ChatGPT status.

## Learn first

This repo is the hands-on companion to [The AI Agent Factory](https://agentfactory.panaversity.org/). Study these lessons from the book **before** you start building this step:

- [16.1 From a prompt you repeat to a skill](https://agentfactory.panaversity.org/building-ai-workers/skills-and-plugins/from-a-prompt-to-a-skill/). What a skill is.
- [20.12 Skills that travel with the server](https://agentfactory.panaversity.org/building-ai-workers/mcp-apps/skills-that-travel-with-the-server/). The Skills over MCP extension.
- [20.13 Approving a skill from a server](https://agentfactory.panaversity.org/building-ai-workers/mcp-apps/approving-a-skill-from-a-server/). How trust and approval work.
- *Optional:* [16.9 Installing is a trust decision](https://agentfactory.panaversity.org/building-ai-workers/skills-and-plugins/installing-is-a-trust-decision/). Why adding a skill is a trust decision.

**Official docs.** Keep these open while you build:

- [MCP: Skills over MCP](https://modelcontextprotocol.io/extensions/skills/overview). How a server provides skills to a client.
- [Extensions client support matrix](https://modelcontextprotocol.io/extensions/client-matrix). Current Claude and ChatGPT support.

## Why this step matters

Tools say *what* a model can do, and skills say *how* to do a job well. Serving skills from the MCP server keeps that expertise versioned next to the tools it describes, so every connected client gets the same playbook.

## Why this technology in an MCP server: Skills over MCP

- **What it is.** A skill is packaged know-how: instructions (and optional files) that teach the model how to do a job well. The Skills over MCP extension lets your server provide skills alongside its tools.
- **Why an MCP server uses it.** Tools say *what* the model can do. Skills say *how* to do a client's job with them, such as "prepare the monthly sales review". Serving skills from the server keeps that playbook versioned next to the tools, and every connected client gets the same one.
- **What it solves.** Long, procedural tool descriptions that bloat the model's context, and inconsistent results because each user prompts differently. Skills load only when needed (progressive disclosure).
- **Alternatives.** Putting the procedure in tool descriptions (costly in context), MCP prompts (templates the user picks), or asking users to install a skill in their own client separately.

## What you will learn

- Understand what a skill is (instructions plus optional resources) and when the model loads one
- Expose skills from the server using the Skills over MCP extension
- Write skills that orchestrate several tools, for example "prepare a monthly sales review"
- Decide what belongs in a tool description versus a skill
- Version and test skills

## What you will build

A `monthly-sales-review` skill that guides the model through querying Neon, choosing the right widgets and writing a summary.

## Key concepts

- **Skills**: Packaged procedural knowledge the model can load on demand.
- **Progressive disclosure**: Short metadata up front, with the full instructions only when needed.
- **Tools + skills**: Capabilities plus a playbook for using them.

## Planned outline

1. What Skills over MCP adds
2. Defining and serving a skill
3. Writing effective skill instructions
4. Skills that drive generative UI
5. Testing skills

## Prerequisites

- [Step 9](../step-09-generative-ui-mcp-apps/)
- The tools and accounts listed in the [main README](../README.md#prerequisites)

## Build it with Claude Code

Every step is built with **Claude Code in Claude Desktop**. Follow the instructions in order and paste each prompt into the **Code** tab of Claude Desktop. Read what Claude proposes before you approve it, because understanding the code is the point. The bundled `build-mcp-server`, `build-mcp-app` and `build-mcpb` skills load automatically in this repo.

> These prompts are a draft and will be refined as the step is developed.

**1. Open the repo's root folder in the Code tab of Claude Desktop so the bundled skills load, then copy your step 9 code into `step-10-skills-over-mcp/`.**

```text
Copy my step-09 code into step-10-skills-over-mcp/ so I can build on it. Copy only the source and config files: skip README.md (this folder already has the course's README, which must not change), NOTES.md, node_modules/, .wrangler/, dist/ and .dev.vars. Then rename the Worker in the wrangler config to learn-mcp-step-10 so it deploys alongside my earlier steps instead of replacing them, run npm install, and confirm the project still builds. Then create a Neon branch named step-10 from my step-09 branch and point this step's database settings (the connection string in .dev.vars and as a secret, and Hyperdrive once the server uses it) at the new branch, so my earlier steps keep working while they are graded.
```

**2. Check the extension's current client support (see the note at the top of this page), then plan.**

```text
Read the Skills over MCP extension docs linked in this step and summarize how a server provides skills to a client. Then plan how to add one to this server.
```

**3. Write the skill.**

```text
Create a monthly-sales-review skill. It should guide the model to pull the right data with get_sales_summary and list_orders, choose the right widgets, and write a short narrative summary with recommendations.
```

**4. Serve it.**

```text
Expose the skill from the server using the Skills over MCP extension, and keep it in a versioned folder next to the tools it uses.
```

**5. Refine tools vs. skills.**

```text
Review the tool descriptions and the skill together. Move procedural how-to guidance out of tool descriptions and into the skill, and keep tool descriptions about what each tool does.
```

**6. Test it.**

```text
Deploy and give me prompts that should trigger the skill in each client. Tell me how to confirm the skill was actually used.
```

## Testing targets

- claude.ai and Claude Desktop (primary)
- ChatGPT (developer mode)

## Submission checklist

Submit through your **fork**, following [SUBMITTING.md](../SUBMITTING.md). ⛔ Do not open a pull request to the course repo.

- [ ] Your fork is synced with the course repo
- [ ] All code for this step is in `step-10-skills-over-mcp/` and pushed to your fork
- [ ] No secrets are committed (`.dev.vars.example` only)
- [ ] The server is deployed to your own Cloudflare account and the `/mcp` URL works
- [ ] Tenant isolation: the skill uses only company-scoped tools, and no company's data is written into the skill
- [ ] It works in claude.ai or Claude Desktop. If Claude doesn't support this extension yet, the rest of the server still works there and your NOTES.md records the support status from the [client support matrix](https://modelcontextprotocol.io/extensions/client-matrix)
- [ ] It works in ChatGPT (developer mode), with the same exception and NOTES.md entry if ChatGPT doesn't support this extension yet
- [ ] Tagged and pushed: `git tag step-10-done && git push origin step-10-done`
- [ ] Submitted in the form: fork URL, tag `step-10-done`, live server URL, and screenshots of the monthly-sales-review skill in use (or a note on client support if it isn't available yet) in **Claude** and **ChatGPT**

## References

- [MCP: Skills over MCP](https://modelcontextprotocol.io/extensions/skills/overview)

---

← [Step 09: Generative UI with MCP Apps](../step-09-generative-ui-mcp-apps/) · [Roadmap](../README.md#roadmap) · [Step 11: Per-User State with Durable Objects](../step-11-durable-objects/) →
