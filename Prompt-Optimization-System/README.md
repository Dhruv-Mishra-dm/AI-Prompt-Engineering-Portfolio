# Prompt Optimization & Guardrail Systems

This directory contains advanced prompt architectures focused on the technical control of Large Language Models (LLMs). The core objective of these systems is to enforce strict output boundaries, prevent hallucinations, and ensure machine-readable formatting for production environments.

## Core Competencies Demonstrated
* **Contextual Grounding:** Building closed-world assumptions for high-stakes Retrieval-Augmented Generation (RAG) pipelines.
* **Schema Enforcement:** Forcing LLMs to abandon conversational filler in favor of strictly typed, parser-safe JSON outputs.
* **Algorithmic Neutrality:** Stripping rhetorical bias and emotional framing from unstructured text to extract purely logical claims.

---

## 📂 Project Index

### 1. [RAG Grounded Answer Engine](./RAG-Grounded-Answer-Engine.md)
An enterprise-grade prompt for Retrieval-Augmented Generation systems. It enforces a strict "Context-Only" boundary, making it highly effective for querying proprietary legal, medical, or technical documentation where accuracy is non-negotiable.

### 2. [Strict JSON Output Enforcer](./Strict-JSON-Enforcer.md)
A machine-readable extraction engine that forces LLMs to output perfectly valid JSON. It utilizes rigorous schema definitions and negative constraints to strip conversational filler, ensuring the output is directly consumable by production APIs without preprocessing. *(Includes benchmark testing across Gemini, Claude, and GPT models).*

### 3. [The Unbiased Summarizer](./Unbiased-Summarizer.md)
An objective analysis engine operating in "Strict Neutralization Mode." This prompt strips emotional bias, persuasive language, and subjective framing from charged texts, extracting only the core logical arguments and verifiable supporting evidence.
