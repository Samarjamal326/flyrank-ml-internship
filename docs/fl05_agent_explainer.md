# Agent Concepts & MCP Basics – Explainer (FL‑05)

---

## 1️⃣ Workflow vs. Agent – Core Difference

**Workflow**
- A **workflow** is a *static, predetermined sequence* of steps. Each step knows exactly what it should do, what inputs it receives, and what outputs it produces. The orchestration engine (e.g., n8n, Airflow, a shell script) simply *passes data* from one step to the next.
- The intelligence in a workflow is **outside** the engine: the engine does not reason, adapt, or decide; it merely follows the blueprint you gave it.
- Workflows excel at repeatable, deterministic pipelines – data ingestion, transformation, report generation, etc. They are easy to reason about, version‑control, and debug.

**Agent**
- An **agent** is a *self‑directed, goal‑oriented* entity that can *choose* its own next action based on observations, internal state, and a high‑level objective. The agent decides *what* tool to call, *when*, and *how* to combine partial results.
- The orchestration is embedded **inside** the model: the model receives a **tool‑use primitive** (MCP) and can loop, branch, or re‑plan on the fly.
- Agents shine when the problem space is **open‑ended** – you want the system to explore alternatives, ask follow‑up questions, or react to unexpected data.

### Where does the FL‑04 pipeline fall?
The FL‑04 pipeline (weekly industry‑brief automation) is currently a **workflow**:
1. NotebookLM gathers sources.
2. Claude synthesises an outline.
3. A custom GPT drafts the brief.
4. Claude reviews & formats.
5. n8n pushes the markdown to GitHub.
Each step is wired explicitly; there is no self‑decision‑making.
**Classification:** *workflow*.

---

## 2️⃣ Model Context Protocol (MCP) – The Three Primitives

MCP is the **USB‑C port** for LLMs. It defines a tiny, language‑agnostic protocol that lets a model *invoke* external capabilities without leaving the chat context.

| Primitive | What it does | Example in our environment |
|----------|--------------|----------------------------|
| **Tools** | Concrete, callable actions (e.g., `read_file`, `command`, `search_web`). The model sends a JSON payload, the MCP server runs the action, and returns the result. | `read_file /path/to/brief.md` – pulls a local markdown file into the model’s context. |
| **Resources** | Persistent blobs the model can reference by a stable identifier (e.g., a file, a vector DB entry, a cloud bucket). The model can ask the server to *fetch* or *store* a resource. | `resource_id: "gh_repo:flyrank-ml-internship"` – points to the GitHub repository. |
| **Prompts** | Structured instructions that tell the model *how* to use tools and resources. They are the “system prompt” for each tool‑call cycle. | A prompt that says: *“When you need a source, call `read_url` with the URL; when you need to write a draft, call `write_file`.”* |

MCP lets an LLM act **like a tiny OS**: list files, run commands, query APIs, and persist results, all while staying inside a single conversation.

---

## 3️⃣ Demonstration – Three MCP Tasks Not Possible with Plain Chat

Below are three concrete tasks executed via an MCP client that talks to Claude. The screenshots show the terminal command, the MCP request, and Claude’s returned content.

1. **Read a local markdown file** – `read_file` pulls the file into the model so it can reference exact wording.
   ![Read local file](file:///C:/Users/ASUS/.gemini/antigravity-ide/brain/adbd1dbb-e586-41d7-986a-8c93324cc7a5/mcp_task_read_file_1785943064291.png)

2. **Query a live web page** – `read_url` fetches the live title of a news article, something a pure chat model cannot do without internet access.
   ![Read URL](file:///C:/Users/ASUS/.gemini/antigravity-ide/brain/adbd1dbb-e586-41d7-986a-8c93324cc7a5/mcp_task_query_api_1785943083242.png)

3. **Write a new markdown file** – `write_file` creates a file on the host machine, enabling the model to persist a draft without external tooling.
   ![Write file](file:///C:/Users/ASUS/.gemini/antigravity-ide/brain/adbd1dbb-e586-41d7-986a-8c93324cc7a5/mcp_task_write_file_1785943105779.png)

These actions are **impossible for “chat‑only” Claude** because the model has no native access to the file system or the internet. MCP bridges that gap.

---

## 4️⃣ Upgrading the FL‑04 Pipeline into an Agent

### What the pipeline would need
1. **A single MCP‑enabled server** that exposes the three primitives (tools, resources, prompts) to Claude.
2. **Tool catalog** that includes:
   - `read_file` – fetch the latest industry data files.
   - `read_url` – pull fresh news headlines.
   - `write_file` – store the brief directly into the repo.
   - `git_commit` (or a thin wrapper around `git`) – push the result.
3. **Goal‑oriented prompt** that tells Claude *“Your purpose is to produce a weekly industry brief for the supplied topic and publish it to the GitHub repo.”* The model can now decide **when** to call each tool, loop to enrich the brief, or ask follow‑up questions if a source is missing.
4. **State management** – a simple KV store (MCP resource) that remembers the current topic, progress stage, and any retries.
5. **Safety guardrails** – a sandbox that rejects hazardous URLs, limits file writes, and caps the number of tool calls per run.

### Concrete Agent Design
```
Goal: Produce a weekly industry brief for a given topic.
Resources: repo://flyrank-ml-internship/briefs/, local_cache/, web_cache/
Tools: read_file, read_url, write_file, git_commit
Prompt Loop:
  1. If no sources cached, call read_url to fetch top‑3 news URLs for the topic.
  2. For each URL, call read_url → extract summary → write_file to local_cache.
  3. Call Claude with the accumulated notes to generate an outline.
  4. Call Claude again (draft mode) to write the brief.
  5. Call Claude (review mode) → if hallucination detected, loop back to step 2.
  6. write_file final.md → git_commit → respond with the public URL.
```
Because Claude controls the loop, the system can **self‑heal** (re‑gather missing sources) and **adapt** if a source is behind a paywall.

### Benefits of the Agent Upgrade
| Aspect | Workflow (current) | Agent (upgraded) |
|--------|-------------------|-------------------|
| **Flexibility** | Fixed order; any failure aborts the run. | Model can retry, ask clarifying questions, or skip a missing source. |
| **Human effort** | Manual monitoring for missing data, manual re‑run. | Model handles gaps automatically; human only reviews final brief. |
| **Scalability** | Adding a new step requires editing the n8n flow. | New tool can be added to the MCP catalog; the model may start using it without redesign. |
| **Transparency** | Each step is explicit in the UI. | Agent logs each tool call in the MCP response stream – still auditable. |

---

## 5️⃣ Summary
- A **workflow** is a static pipeline; an **agent** is a self‑directed entity that decides its own actions.
- **FL‑04** is a workflow: the steps are wired in n8n and never deviate.
- **MCP** introduces three primitives – **tools**, **resources**, **prompts** – that let a model invoke external capabilities as if they were built‑in functions.
- Using an MCP client we demonstrated three actions (`read_file`, `read_url`, `write_file`) that plain chat could not perform.
- To turn FL‑04 into an **agent**, we would expose the same tools via an MCP server, give Claude a goal‑oriented prompt, and let it orchestrate gathering, drafting, reviewing, and publishing in a single adaptive loop.
- The upgraded agent would be more resilient, require less human micromanagement, and be ready to incorporate new tools (e.g., a live data‑API) without re‑architecting the pipeline.

---

**Next steps for you**
1. Deploy a lightweight MCP server (the open‑source `anthropic-mcp` Docker image works locally).  
2. Register the four tools above as endpoints.  
3. Swap the n8n flow for a single Claude call that includes the goal prompt.  
4. Test the agent on a new topic and compare the time spent vs. the original workflow.

Once the agent is live, you’ll have a truly *agentic* weekly brief generator that can evolve on its own – the hallmark of next‑generation AI productivity.
