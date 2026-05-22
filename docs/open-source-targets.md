# Open Source Targets

Goal: find realistic external repos for 5 useful PRs in 30 days. Contributions should be small, inspectable, and useful to maintainers.

## Candidate Repos

| Repo | Why It Matches | Issue Type To Look For | Likely PR Type | Difficulty | Link |
| --- | --- | --- | --- | --- | --- |
| LangChain | Agent and RAG ecosystem with many docs and examples | Broken docs, example drift, reproducibility issues | Docs/example fix | Medium | https://github.com/langchain-ai/langchain |
| LangGraph | Directly aligned with agent workflows and durable state | Missing examples, unclear persistence docs, test gaps | Docs/example/test | Medium | https://github.com/langchain-ai/langgraph |
| LlamaIndex | RAG framework with document loaders and retrieval examples | Loader docs, broken notebooks, evaluation examples | Docs/example cleanup | Medium | https://github.com/run-llama/llama_index |
| Haystack | RAG pipelines and document search | Tutorial drift, docs clarity, reproducible examples | Docs/setup fix | Medium | https://github.com/deepset-ai/haystack |
| Docling | Document AI and PDF conversion | PDF examples, setup notes, bug reproductions | Docs/repro/test | Medium | https://github.com/docling-project/docling |
| Unstructured | Document parsing and ingestion | Docs, examples, file-type edge cases | Docs/repro fix | Medium | https://github.com/Unstructured-IO/unstructured |
| Chroma | Vector database used in RAG prototypes | Example cleanup, docs gaps, TypeScript/Python snippets | Docs/example | Low-Medium | https://github.com/chroma-core/chroma |
| Qdrant examples/docs | Vector search and hybrid retrieval examples | Example drift, broken links, retrieval tutorials | Docs/example | Low-Medium | https://github.com/qdrant/qdrant |
| Django REST framework | Backend/API engineering relevance | Docs clarity, small tests, reproduction notes | Docs/test | Medium | https://github.com/encode/django-rest-framework |
| FastAPI | Backend examples and docs | Example clarity, docs fixes, test snippets | Docs/example | Low-Medium | https://github.com/fastapi/fastapi |

## PR Types To Prioritize

- Docs improvements.
- Setup or reproduction fixes.
- Broken link fixes.
- Example cleanup.
- Small tests.
- Small bugfixes.
- Type fixes.
- README clarity improvements.

## Selection Rule

Pick issues where I can reproduce the problem locally, explain the fix in one paragraph, and keep the diff small enough for a maintainer to review quickly.

## Sprint Run Log

### 2026-05-21

Daily OSS Scout + Contributor one-off run after automation update.

Candidate selected:

| Repo | Issue/PR | Type | Status | Notes |
| --- | --- | --- | --- | --- |
| `Aristocles/klebb` | https://github.com/Aristocles/klebb/issues/254 -> https://github.com/Aristocles/klebb/pull/269 | Docs correctness | PR opened | Fixed README recipe count from 10 to 12 after verifying `docs/RECIPES.md` contains 12 numbered recipes. |

Score:

| Criterion | Score | Notes |
| --- | --- | --- |
| Relevance | 3.5 | LLM-first, file-driven dashboard with docs/manifest workflow; adjacent to product systems and AI tooling. |
| Issue clarity | 5 | Issue identified exact file, line, and expected change. |
| Change size | 5 | One focused README correction. |
| Acceptance likelihood | 4 | Labeled `good first issue`, `documentation`, and `area:docs`; no duplicate PR found. |
| Local verification | 5 | Verified README line, counted numbered recipes, and ran `git diff --check`. |

Verification:

```bash
rg "docs/RECIPES.md.*copy-pasteable" -n README.md
rg "^## Recipe [0-9]+" -n docs/RECIPES.md | Measure-Object | Select-Object -ExpandProperty Count
git diff --check
```

`npm test` was not run because the change is docs-only.

Previous manual validation run:

Daily Codex automation logic was run manually once to validate the workflow.

Searches performed:

- `fastapi/fastapi`: no low-risk docs/example issues found in the first pass.
- `langchain-ai/langgraph`: found many active external issues, but most are bug/security/runtime reports that need reproduction before touching code.
- `run-llama/llama_index`: found several RAG/evaluation/documentation-adjacent issues.
- `qdrant/qdrant`: found API/docs/diagnostic candidates, mostly requiring careful reproduction.

Shortlist:

| Repo | Issue/PR | Type | Status | Notes |
| --- | --- | --- | --- | --- |
| `run-llama/llama_index` | https://github.com/run-llama/llama_index/issues/21626 | Docs/catalog | Candidate | Catalog/docs listing for `llama-index-readers-cvfile`; likely small if repo structure is clear. |
| `run-llama/llama_index` | https://github.com/run-llama/llama_index/issues/21549 | Docs/dependency clarity | Candidate | Hugging Face extra reference may be docs/package metadata cleanup; verify before editing. |
| `qdrant/qdrant` | https://github.com/qdrant/qdrant/issues/8412 | OpenAPI docs | Candidate | Missing defaults in OpenAPI spec; likely focused if defaults can be identified from schema/code. |
| `langchain-ai/langgraph` | https://github.com/langchain-ai/langgraph/issues/7844 | Docs/safety guidance | Watch | Aligned with agent-state positioning, but needs maintainer signal before writing broad guidance. |

Outcome:

No external PR was opened in this run. The automation correctly avoided forcing a low-quality contribution when the first-pass candidates required repository-specific verification.

### 2026-05-22

Daily OSS Scout + Contributor (automation run #1).

Candidate selected:

| Repo | Issue/PR | Type | Status | Notes |
| --- | --- | --- | --- | --- |
| `docling-project/docling-mcp` | https://github.com/docling-project/docling-mcp/issues/58 | Docs/tool-spec clarity | Blocked | Issue requests clarifying `create_docling_document` / document-creation tooling so LLMs don’t try to inline an entire document into one tool call. |

Score:

| Criterion | Score | Notes |
| --- | --- | --- |
| Relevance | 5 | Direct overlap: MCP + agent workflows + document AI. |
| Issue clarity | 4 | Clear desired outcome (reduce ambiguity / prevent misuse); requires reading existing tool schemas. |
| Change size | 4 | Likely a small doc/tool-description update + maybe one example. |
| Acceptance likelihood | 4 | Maintainer-aligned (improves correctness and user experience); narrow scope. |
| Ability to verify locally | 2 | Local verification blocked by inability to clone/run checks in this environment. |

Blockers encountered:

- Outbound `git clone` to `github.com:443` failed from this environment.
- `gh` CLI auth for account `42amps` is currently invalid, so we can’t fork/push via CLI.
- Available GitHub connector tooling can read public files/issues, but does not expose an action to create a fork, which is required for external PRs.

Next steps (to unblock PRs in future runs):

1. Fix `gh` auth for `42amps` (refresh token) and/or enable outbound `github.com:443` for `git clone`.
2. Add/enable a GitHub connector capability that can fork repositories (GitHub REST `POST /repos/{owner}/{repo}/forks`), or manually pre-create forks for 2–3 target repos (e.g. `docling-project/docling-mcp`, `run-llama/llama_index`, `langchain-ai/langgraph`) so branch+PR creation is possible with existing tools.

### 2026-05-22

Daily OSS Scout + Contributor manual execution after automation setup.

Environment check:

- `gh auth status` is valid for `42amps` with `repo` and `workflow` scopes.
- Existing external PR remains open: https://github.com/Aristocles/klebb/pull/269.

Searches performed:

- `Aristocles/klebb` documentation issues.
- `docling-project/*` good-first issues.
- `run-llama/LlamaIndexTS` good-first/help-wanted issues.
- `langchain-ai/langgraph` documentation issues.
- `qdrant/qdrant` documentation issues.

Shortlist:

| Repo | Issue/PR | Type | Status | Notes |
| --- | --- | --- | --- | --- |
| `run-llama/LlamaIndexTS` | https://github.com/run-llama/LlamaIndexTS/issues/2016 | Docs/API usage | Candidate | Documents passing a custom `embedModel` or `llm` per request instead of relying on global `Settings`; highly relevant to RAG/product systems, but needs repo checkout and docs structure review before editing. |
| `docling-project/docling` | https://github.com/docling-project/docling/issues/3128 | Document serialization | Candidate | Footnote serialization in markdown output; relevant to document AI, but likely requires local reproduction and tests before a PR. |
| `docling-project/docling` | https://github.com/docling-project/docling/issues/3094 | API/docs example | Candidate | `image_dir` parameter for markdown export; promising if maintainers expect implementation, but not safe as docs-only without reading current serializer behavior. |
| `langchain-ai/langgraph` | https://github.com/langchain-ai/langgraph/issues/6239 | Docs/runtime guidance | Watch | Relevant to checkpointing and Postgres limits, but issue likely needs reproduction and maintainer direction before changing docs. |

Score for top candidate (`run-llama/LlamaIndexTS#2016`):

| Criterion | Score | Notes |
| --- | --- | --- |
| Relevance | 5 | Direct overlap with RAG, LLM configuration, and retrieval workflows. |
| Issue clarity | 4 | Clear documentation need, but exact docs location must be confirmed. |
| Change size | 4 | Likely one docs section/example if the API supports this cleanly. |
| Acceptance likelihood | 4 | Labeled `documentation`, `good first issue`, and `help wanted`. |
| Ability to verify locally | 3 | Requires checkout and package/docs command discovery; feasible but not completed in this short validation run. |

Outcome:

No PR was opened in this validation run. The automation correctly stopped at scouting because a useful PR needs a repo checkout, docs-location verification, and local command discovery. Next run should start with `run-llama/LlamaIndexTS#2016`, read `CONTRIBUTING.md`, find the LLM/settings docs, and only open a PR if the example can be verified locally.
