# Knowledge Graphs for Retrieval

Vector search and graph retrieval solve different parts of the retrieval problem.

## What Vector Search Is Good At

Vector search is good at fuzzy semantic matching. It can find passages that are similar in meaning even when they use different words.

It is useful for:

- Natural-language questions.
- Conceptual similarity.
- Finding relevant paragraphs.
- Searching noisy or unstructured text.

## What Graph Retrieval Is Good At

Graph retrieval is good at relationships. A graph can represent entities, links, dependencies, provenance, and multi-hop paths.

It is useful for:

- Entity-centric questions.
- Relationship traversal.
- Dependency chains.
- Cross-document connections.
- Questions where "how are these things connected?" matters.

## Entities and Relationships

A knowledge graph usually has entities and edges:

- Entities: people, companies, documents, functions, APIs, projects, clauses.
- Relationships: owns, depends on, references, contradicts, implements, pays, blocks.

The value comes from making relationships explicit enough to traverse.

## When Knowledge Graphs Help RAG

Graphs can help when vector search retrieves relevant text but misses structure:

- Legal or policy documents with cross-references.
- Codebases with dependencies.
- Research corpora with papers, authors, methods, and datasets.
- Product systems where entities have state and relationships.

## Hybrid Retrieval

A practical pattern is vector search plus graph traversal:

1. Use vector search to find semantically relevant entry points.
2. Extract entities from those results.
3. Traverse graph relationships around those entities.
4. Rerank or filter the combined evidence.
5. Generate an answer grounded in both text and relationships.

## Probabilistic Filters

Probabilistic filters can fit as a cheap pre-filter or routing layer. For example, a system can estimate which documents, entities, or graph neighborhoods are likely worth deeper retrieval before running expensive reranking or generation.

## Tradeoffs

Graphs require schema decisions, extraction quality, maintenance, and debugging. Vector search is easier to start with, but it can hide relationship failures. Hybrid systems add complexity, so they should be justified by real failure cases.

The best reason to add a graph is not trend-chasing. It is a repeated retrieval failure that relationship structure can solve.
