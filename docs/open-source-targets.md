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
