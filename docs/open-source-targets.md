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
