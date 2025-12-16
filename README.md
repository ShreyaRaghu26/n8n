Flowise Tool-Augmented LLM Agent

This repository contains a Flowise chatflow implementing a tool-using Large Language Model (LLM) agent capable of retrieval-augmented generation (RAG), web search, reranking, and multi-turn conversational memory.

The system dynamically routes user queries to the appropriate tools based on intent, combining document retrieval and web search within a single agent-driven architecture.

What This Project Does

Builds a tool-augmented LLM agent using Flowise

Implements Retrieval-Augmented Generation (RAG) over uploaded documents

Uses vector search + neural reranking for improved retrieval quality

Integrates web search as an external tool

Maintains conversation memory for multi-turn interactions

Enforces strict tool-routing rules through system-level prompt design

System Architecture
1. Document Ingestion & Indexing

Documents are loaded using a File Loader node

Text is split using a Recursive Character Text Splitter

Chunk size: 1000 characters

Overlap: 200 characters

Text chunks are embedded using OpenAI Embeddings (text-embedding-3-large, 3072 dimensions)

Embeddings are stored in a Pinecone vector database

2. Retrieval & Reranking

Initial semantic retrieval is performed using Pinecone similarity search

Retrieved documents are passed through a Jina AI Reranker (jina-reranker-v2-base-multilingual)

Top-ranked results are selected for downstream use by the agent

3. Tool Layer

The agent has access to multiple tools:

Retriever Tool

Wraps the Pinecone + Jina retriever

Used for document-based questions

Tavily API Tool

Performs external web searches

Used for open-web lookup queries

Tool usage is controlled by explicit routing rules defined in the system prompt.

4. LLM Agent

Built using ChatOpenAI (gpt-4o-mini)

Uses function/tool calling to decide which tool to invoke

Operates under a detailed system message that defines:

When each tool should be used

How results should be processed

What to do when information is missing

5. Conversational Memory

Uses Buffer Memory to store chat history

Enables contextual follow-up questions

Supports multi-turn reasoning across interactions

Response Behavior

Every agent response:

Uses tools only when required

Avoids fabricating external information

Returns structured, grounded answers

Includes:

Two relevant follow-up questions

A confidence score (0–100%) indicating answer certainty

Technologies Used

Flowise – visual LLM orchestration

OpenAI Chat Models & Embeddings

Pinecone – vector database

Jina AI Reranker – neural reranking

Tavily API – web search tool

Tool-Calling LLM Agent

Recursive Text Splitting

Conversation Memory

Use Cases

Tool-augmented conversational agents

Retrieval-based question answering

Hybrid systems combining RAG and web search

Demonstrating agent routing and orchestration patterns

Learning Flowise-based LLM system design

How to Use

Import the provided Chatflow JSON into Flowise

Configure API credentials (OpenAI, Pinecone, Jina AI, Tavily)

Upload documents for indexing (optional)

Start chatting with the agent

Notes

This project focuses on system orchestration, not model training

All retrieval and search behavior is governed by prompt-level routing rules

Designed for clarity, correctness, and tool safety

Author

Built by Shreya Raghunath as a hands-on implementation of tool-augmented LLM systems using
