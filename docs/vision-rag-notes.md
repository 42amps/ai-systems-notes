# Vision-RAG Notes

Vision-RAG treats document pages as visual artifacts instead of reducing every file to OCR text before retrieval.

## OCR-First RAG

OCR-first RAG usually follows this path:

1. Extract text from a PDF or scanned image.
2. Chunk the text.
3. Embed chunks.
4. Retrieve chunks for a query.
5. Generate an answer from retrieved text.

This works well when the document is mostly clean text in a simple reading order.

## Where OCR-First Pipelines Fail

OCR-first systems often lose structure before retrieval starts:

- Tables become disconnected text fragments.
- Charts lose the visual relationship between labels, axes, and values.
- Scanned PDFs introduce recognition errors.
- Layout-heavy documents can be read in the wrong order.
- Mixed-script documents can produce inconsistent extraction quality.
- Forms can detach labels from the values they describe.

Once that structure is lost, the retriever may never see the evidence needed to answer correctly.

## Page-Level Retrieval

Page-level retrieval embeds rendered pages or page images. Instead of asking "which text chunk matches this query?", the retriever asks "which page image is visually and semantically relevant?"

This can be useful for:

- Tables and reports.
- Scientific PDFs.
- Government forms.
- Financial statements.
- Slide decks.
- Scanned or layout-heavy documents.

## ColPali / ColQwen-Style Retrieval

ColPali and ColQwen-style systems use multimodal models to represent document pages visually. At a high level, they compare a text query with visual page embeddings, often using late-interaction retrieval ideas inspired by ColBERT-like approaches.

The useful idea is not "OCR is bad." The useful idea is that some document questions require visual layout, and retrieval should preserve that signal long enough to use it.

## Open Questions

- When is text-only retrieval enough?
- When is page-level visual retrieval worth the extra cost?
- How should retrieved pages be evaluated?
- How do we handle long documents without huge latency?
- How should visual retrieval combine with OCR text, metadata, and section structure?

## Status

Conceptual notes. No benchmark results are claimed here.
