# Retrieval-Augmented-Generation-under-Knowledge-Edits-RAG-System-
This project implements a full Retrieval-Augmented Generation (RAG) pipeline that can reason correctly when the underlying knowledge base has been edited. It simulates real-world scenarios where facts change (e.g., dynamic databases, evolving knowledge graphs, misinformation corrections). The system retrieves modified Wikidata facts and uses a generator LLM to answer multi-step reasoning questions based solely on the updated facts, overriding the model’s prior knowledge.

## Motivation
Large Language Models struggle when:
1. Facts change after pretraining
2. Entities have updated properties
3. Reasoning depends on modified relationships
This project studies how RAG can fix outdated internal model knowledge by providing externally retrieved facts.

## Key Features
#### 1. Retrieval Component
1. Implemented BM25 lexical retriever
2. Implemented dense embedding retriever using:
    2.1 Qwen/Qwen3-Embedding-0.6B
    2.2 hkunlp/instructor-large
3. Evaluated Hit@K (1, 2, 4, 8, 16, 32, 64)
4. Achieved ~87% Hit@1 with dense embeddings

#### 2. Generator Component
1. Integrated small LLMs using vLLM:
    1.1 HuggingFaceTB/SmolLM3-3B
    1.2 Qwen/Qwen2.5-3B-Instruct
2. Designed strictly structured system + user prompts
3. Added step-by-step reasoning section for interpretable outputs

#### 3. Full RAG Pipeline
1. Retrieval → Context Selection → Prompt Construction → LLM Answering → JSON Parsing
2. Experiments with:
    K = 0 (no retrieval baseline)
    K ≥ 1 (RAG-enhanced reasoning)
3. Demonstrated that RAG greatly improves performance vs. no retrieval.
