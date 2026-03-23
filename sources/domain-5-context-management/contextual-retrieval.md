# Contextual Retrieval
Source: https://www.anthropic.com/news/contextual-retrieval

## The Problem
Traditional RAG splits documents into chunks that lose context. A chunk saying "revenue grew by 3%" doesn't specify which company or time period.

## The Solution: Contextual Retrieval
Prepend chunk-specific explanatory context to each chunk before embedding (Contextual Embeddings) and creating BM25 index (Contextual BM25).

Example transformation:
- Original: "The company's revenue grew by 3% over the previous quarter."
- Contextualized: "This chunk is from an SEC filing on ACME corp's performance in Q2 2023; the previous quarter's revenue was $314 million. The company's revenue grew by 3% over the previous quarter."

## Implementation
Use Claude to generate context for each chunk (~50-100 tokens prepended).
With prompt caching: one-time cost of $1.02 per million document tokens.

## BM25 + Embeddings
- BM25: lexical matching for exact terms (error codes, technical terms)
- Embeddings: semantic similarity
- Combine both with rank fusion for best results

## Performance Results
- Contextual Embeddings alone: 35% reduction in retrieval failure
- Contextual Embeddings + Contextual BM25: 49% reduction
- With Reranking added: 67% reduction (5.7% -> 1.9%)

## Key Takeaways
1. Embeddings + BM25 > embeddings alone
2. Adding context to chunks improves accuracy significantly
3. Reranking further improves results
4. All benefits stack
5. Use top-20 chunks (better than top-5 or top-10)

## Note on Simple Approach
If knowledge base < 200K tokens (~500 pages), just include it all in the prompt with prompt caching.
