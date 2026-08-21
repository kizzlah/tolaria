---
type: Note
---
# Ollama Models + Pi Agent

> [!info]
> I had initially provided Pi with a list of my models installed at the start of this session to gain its opinion on which models I should remove as they were redundant to keep for whatever reason. After specifying to overlook any "cloud" variant models, Pi provided a table with its suggestions:

| **Model (ID)** | **Size** | **Use-case** |
| --- | --- | --- |
| llama3.1:8b (46e0c10c039e) | 4.9 G | Primary, all-round LLM |
| phi4-mini:3.8b (78fad5d182a7) | 2.5 G | Strong compact LLM |
| qwen2.5-coder:1.5b-base (02e0f2817a89) | 986 M | Code-completion / programming |
| nomic-embed-text:latest (0a109f422b47) | 274 M | Tiny embedding for similarity / search |
| llama3.2:3b (a80c4f17acd5) | 2.0 G | Sub-2 GB general-purpose fallback |
| mxbai-embed-large:latest (468836162de7) | 669 M | Higher-quality embeddings if you need them |

> [!info]
> After a brief discussion on which embredding model to actual  keep - the consensus being both - I prompted Pi to suggestion models I should consider adding to round out my roster. The following is the exact output Pi generated from the terminal session:
