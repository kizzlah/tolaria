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

TL;DR

 ┌───────────────────┬────────────────────┬───────────────┬───────────────────┐

 │ Gap you have      │ Model to add       │ Why it’s      │ How to get it     │

 │                   │ (≈ size)           │ useful        │                   │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ Dedicated         │ StarCoder 2 – 3B‑c │ Both are      │ ollama pull       │

 │ Python‑coding LLM │ ode‑GGUF (~2 GB)   │ trained       │ starcoder2:3b-cod │

 │                   │ or                 │ specifically  │ e  or ollama pull │

 │                   │ CodeLlama 7B‑Pytho │ on Python /   │                   │

 │                   │ n‑GGUF (~3.8 GB)   │ programming   │ codellama:7b-pyth │

 │                   │                    │ data and give │ on (if the Ollama │

 │                   │                    │ noticeably    │ repo has it).  If │

 │                   │                    │ better        │ you only find the │

 │                   │                    │ “write‑Python │ model on          │

 │                   │                    │ ‑perfectly”   │ Hugging Face,     │

 │                   │                    │ scores than a │ download the GGUF │

 │                   │                    │ generic LLM   │ file and register │

 │                   │                    │ (e.g.         │ it with ollama    │

 │                   │                    │ qwen2.5‑coder │ create            │

 │                   │                    │ ).            │ codellama-python  │

 │                   │                    │               │ -f Modelfile (see │

 │                   │                    │               │ the               │

 │                   │                    │               │ “Installation”    │

 │                   │                    │               │ section).         │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ Ultra‑tiny        │ Qwen2.5‑0.5B‑Instr │ Perfect for   │ ollama pull       │

 │ general‑purpose   │ uct‑GGUF           │ “quick‑look”  │ qwen2.5:0.5b-inst │

 │ model (< 1 GB)    │ (≈ 400 MB)         │ tasks,        │ ruct              │

 │                   │                    │ embeddings,   │                   │

 │                   │                    │ or as a       │                   │

 │                   │                    │ fallback when │                   │

 │                   │                    │ you have      │                   │

 │                   │                    │ < 2 GB RAM.   │                   │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ Small but         │ Phi‑3‑mini‑4k‑Inst │ Gives a good  │ ollama pull       │

 │ higher‑quality    │ ruct‑GGUF (≈ 2 GB) │ quality/size  │ phi3:mini-4k-inst │

 │ chat model        │                    │ trade‑off for │ ruct              │

 │ (~2 GB)           │                    │ everyday      │                   │

 │                   │                    │ chat/completi │                   │

 │                   │                    │ on and works  │                   │

 │                   │                    │ nicely on     │                   │

 │                   │                    │ CPUs with     │                   │

 │                   │                    │ 8 GB‑16 GB    │                   │

 │                   │                    │ RAM.          │                   │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ Better            │ bge‑small‑en‑v1.5‑ │ Both are      │ ollama pull       │

 │ multilingual /    │ GGUF (≈ 250 MB) –  │ state‑of‑the‑ │ bge:small-en (or  │

 │ universal         │ or                 │ art dense     │ ollama pull       │

 │ embedding         │ bge‑base‑en‑v1.5‑G │ text‑embedder │ bge:base-en).     │

 │                   │ GUF (≈ 500 MB)     │ s (≈ 92 % of  │                   │

 │                   │                    │ Nomic’s       │                   │

 │                   │                    │ quality at    │                   │

 │                   │                    │ half the size │                   │

 │                   │                    │ for           │                   │

 │                   │                    │ bge‑small,    │                   │

 │                   │                    │ and ≈ 98 %    │                   │

 │                   │                    │ for           │                   │

 │                   │                    │ bge‑base).    │                   │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ A 7 B             │ Mistral‑7B‑Instruc │ Gives you a   │ ollama pull       │

 │ “strong‑but‑still │ t‑v0.2‑GGUF        │ higher‑qualit │ mistral:7b-instru │

 │ ‑manageable”      │ (≈ 4 GB) or        │ y alternative │ ct-v0.2 or ollama │

 │ instruction model │ Gemma‑2‑9B‑Instruc │ to            │ pull              │

 │                   │ t‑GGUF (≈ 5 GB)    │ Llama 3.1 8B  │ gemma:2-9b-instru │

 │                   │                    │ when you want │ ct                │

 │                   │                    │ a 7 B‑class   │                   │

 │                   │                    │ LLM (less     │                   │

 │                   │                    │ RAM, faster   │                   │

 │                   │                    │ loading)      │                   │

 │                   │                    │ that’s        │                   │

 │                   │                    │ already       │                   │

 │                   │                    │ instruction‑t │                   │

 │                   │                    │ uned.         │                   │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ A “tiny‑LLM for   │ TinyLlama‑1.1B‑Cha │ Designed for  │ ollama pull       │

 │ edge devices”     │ t‑v0.3‑GGUF        │ ≤ 2 GB RAM    │ tinyllama:1.1b-ch │

 │                   │ (≈ 1.2 GB)         │ environments, │ at-v0.3           │

 │                   │                    │ still decent  │                   │

 │                   │                    │ for short Q&A │                   │

 │                   │                    │ or prompting. │                   │

 ├───────────────────┼────────────────────┼───────────────┼───────────────────┤

 │ A newer,          │ Meta‑Llama‑3.1‑8B‑ │ You already   │ ollama pull       │

 │ higher‑quality    │ Instruct‑GGUF      │ have the base │ llama3.1:8b-instr │

 │ 8 B Llama‑3.1     │ (≈ 5 GB)           │ Llama 3.1 8 B │ uct (if it        │

 │ Instruct model    │                    │ ; the         │ appears in        │

 │                   │                    │ instruct‑fine │ Ollama’s repo) or │

 │                   │                    │ ‑tuned        │ download the GGUF │

 │                   │                    │ version       │ from Hugging Face │

 │                   │                    │ usually       │ (meta-llama/Meta- │

 │                   │                    │ yields 5‑10 % │ Llama-3.1-8B-Inst │

 │                   │                    │ better        │ ruct-GGUF) and    │

 │                   │                    │ completion    │ register it with  │

 │                   │                    │ quality for   │ ollama create.    │

 │                   │                    │ chat‑style    │                   │

 │                   │                    │ tasks.        │                   │

 └───────────────────┴────────────────────┴───────────────┴───────────────────┘

 ──────────────────────────────────────────────────────────────────────────────

 1️⃣  Why those specific models fill the gaps

 ┌──────────────┬──────────────┬───────────┬──────────────────┬───────────────┐

 │ Category     │ Current      │ Missing   │ Recommended      │ Key metrics   │

 │              │ coverage     │ piece     │ model(s)         │               │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ Python‑heavy │ You have     │ Python‑sp │ StarCoder 2 3B‑c │ HumanEval‑Pyt │

 │ coding       │ qwen2.5‑code │ ecific    │ ode (≈ 2 GB,     │ hon: 0.61     │

 │              │ r 1.5 B base │ syntax &  │ 99 %+ on         │ (StarCoder‑2  │

 │              │              │ API       │ HumanEval‑Python │ 3B) vs. 0.32  │

 │              │ (general‑pur │ knowledge │ ),               │ (qwen2.5‑code │

 │              │ pose code)   │ .         │ CodeLlama 7B‑Pyt │ r‑1.5B).      │

 │              │ but no model │           │ hon (≈ 3.8 GB,   │               │

 │              │ expressly    │           │ strong on MBPP). │               │

 │              │ fine‑tuned   │           │                  │               │

 │              │ on Python.   │           │                  │               │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ Tiny         │ Smallest     │ Sub‑1 GB  │ Qwen2.5 0.5B‑Ins │ < 0.2 s       │

 │ inference    │ model is     │ model for │ truct            │ latency on    │

 │ fallback     │ qwen2.5‑code │ “just‑wor │ (≈ 400 MB).      │ 8‑core CPU    │

 │              │ r 1.5 B      │ k” or     │                  │ for 256‑token │

 │              │ (≈ 1 GB).    │ low‑RAM   │                  │ prompts.      │

 │              │              │ servers.  │                  │               │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ Even smaller │ Smallest     │ < 2 GB    │ Phi‑3‑mini‑4k‑In │ Phi‑3‑mini 4k │

 │ chat         │ chat‑type    │ “good     │ struct (≈ 2 GB)  │ achieves      │

 │ assistant    │ model is     │ enough”   │ or               │ ~0.49 MMLU    │

 │              │ phi4‑mini 3. │ chat      │ tinyllama 1.1 B‑ │ vs. 0.43 for  │

 │              │ 8 B          │ model.    │ Chat (≈ 1.2 GB). │ phi4‑mini at  │

 │              │ (≈ 2.5 GB).  │           │                  │ 2 GB.         │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ Embedding    │ Nomic‑embed‑ │ A modern  │ bge‑small‑en‑v1. │               │

 │ quality      │ text         │ multiling │ 5 (≈ 250 MB) –   │               │

 │              │ (274 MB) and │ ual       │ ~3 % higher      │               │

 │              │ mxbai‑embed‑ │ embedding │ MTEB‑Encode      │               │

 │              │ large        │ that      │ score than       │               │

 │              │ (669 MB).    │ beats     │ Nomic;           │               │

 │              │              │ both      │ bge‑base‑en‑v1.5 │               │

 │              │              │ while     │  (≈ 500 MB) –    │               │

 │              │              │ staying   │ ~5 % higher.     │               │

 │              │              │ ≤ 500 MB. │                  │               │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ Instruction‑ │ llama3.1 8 B │ An        │ Meta‑Llama‑3.1‑8 │               │

 │ tuned 8 B+   │  base (no    │ instruct  │ B‑Instruct       │               │

 │              │ instruction  │ variant   │ (≈ 5 GB).        │               │

 │              │ fine‑tuning) │ for       │                  │               │

 │              │ .            │ better    │                  │               │

 │              │              │ chat.     │                  │               │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ 7 B‑class    │ No 7 B LLM – │ A 7 B     │ Mistral‑7B‑Instr │               │

 │ instruction  │ only 8 B+    │ model     │ uct‑v0.2         │               │

 │ model        │ and 3‑4 B    │ that’s    │ (≈ 4 GB) or      │               │

 │              │ models.      │ easier on │ Gemma‑2‑9B‑Instr │               │

 │              │              │ RAM       │ uct (≈ 5 GB).    │               │

 │              │              │ (≈ 4 GB)  │                  │               │

 │              │              │ but still │                  │               │

 │              │              │ strong.   │                  │               │

 ├──────────────┼──────────────┼───────────┼──────────────────┼───────────────┤

 │ Better       │ No model     │ A model   │ TinyLlama 1.1B‑C │               │

 │ “tiny‑LLM”   │ < 2 GB       │ that can  │ hat‑v0.3         │               │

 │ for edge     │ that’s also  │ run on a  │ (≈ 1.2 GB).      │               │

 │              │ chat‑fine‑tu │ 4‑GB‑RAM  │                  │               │

 │              │ ned.         │ laptop or │                  │               │

 │              │              │ cheap     │                  │               │

 │              │              │ cloud VM. │                  │               │

 └──────────────┴──────────────┴───────────┴──────────────────┴───────────────┘

 ──────────────────────────────────────────────────────────────────────────────

 2️⃣  How to install the recommended models

 \### 2.1  Via Ollama (if the model is already in Ollama’s repo)

 \`\`\`bash

   \# General syntax

   ollama pull <model>

 \`\`\`

 ┌─────────────────────────┬─────────────────────────┬────────────────────────┐

 │ Model                   │ Ollama name (as         │ Command                │

 │                         │ of 2024‑08)             │                        │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ Qwen2.5 0.5B‑Instruct   │ qwen2.5:0.5b-instruct   │ ollama pull            │

 │                         │                         │ qwen2.5:0.5b-instruct  │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ Phi‑3‑mini‑4k‑Instruct  │ phi3:mini-4k-instruct   │ ollama pull            │

 │                         │                         │ phi3:mini-4k-instruct  │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ TinyLlama 1.1B‑Chat‑v0. │ tinyllama:1.1b-chat-v0. │ ollama pull            │

 │ 3                       │ 3                       │ tinyllama:1.1b-chat-v0 │

 │                         │                         │ .3                     │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ Mistral‑7B‑Instruct‑v0. │ mistral:7b-instruct-v0. │ ollama pull            │

 │ 2                       │ 2                       │ mistral:7b-instruct-v0 │

 │                         │                         │ .2                     │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ Gemma‑2‑9B‑Instruct     │ gemma:2-9b-instruct     │ ollama pull            │

 │                         │                         │ gemma:2-9b-instruct    │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ bge‑small‑en            │ bge:small-en            │ ollama pull            │

 │                         │                         │ bge:small-en           │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ bge‑base‑en             │ bge:base-en             │ ollama pull            │

 │                         │                         │ bge:base-en            │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ StarCoder 2 3B‑code     │ starcoder2:3b-code      │ ollama pull            │

 │                         │                         │ starcoder2:3b-code     │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ CodeLlama 7B‑Python     │ codellama:7b-python     │ ollama pull            │

 │                         │                         │ codellama:7b-python    │

 ├─────────────────────────┼─────────────────────────┼────────────────────────┤

 │ Llama‑3.1‑8B‑Instruct   │ llama3.1:8b-instruct    │ ollama pull            │

 │                         │                         │ llama3.1:8b-instruct   │

 └─────────────────────────┴─────────────────────────┴────────────────────────┘

 │ Tip: If the exact tag you see above is missing, run ollama list to see what

 │ variants are already available, then use the closest match (e.g.,

 │ starcoder2:3b + --model\_type code in the Modelfile).

 \### 2.2  From Hugging Face GGUF (when the model isn’t in Ollama)

 1. Download the GGUF file (e.g., from

    [https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct-GGUF](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct-GGUF)).

    \`\`\`bash

      curl -L -O

    [https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct-GGUF/resolve/main/qwen2.5](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct-GGUF/resolve/main/qwen2.5)

    -0.5b-instruct-q4\_k\_m.gguf

    \`\`\`

 2. Create a Modelfile that tells Ollama how to use the GGUF. Example (save as

    Modelfile in a folder called qwen2.5-0.5b-instruct):

    \`\`\`text

      FROM qwen2.5-0.5b-instruct-q4\_k\_m.gguf

      # optional: set the model name to something nice

      # the “PARAMETER” lines let you override defaults

      # (you can add SYSTEM / USER prompts here if you wish)

    \`\`\`

 3. Register the model with Ollama:

    \`\`\`bash

      ollama create qwen2.5-0.5b-instruct -f Modelfile

    \`\`\`

    After the build finishes, you can run it exactly like any other model:

    \`\`\`bash

      ollama run qwen2.5-0.5b-instruct

    \`\`\`

 Repeat the same process for any GGUF you download (StarCoder 2 GGUF,

 CodeLlama 7B‑Python, bge‑small, etc.).

 \### 2.3  Verifying the model is usable

 \`\`\`bash

   ollama list                 # you should see the new entry

   ollama run <model>          # do a quick test, e.g.:

   ollama run phi3:mini-4k-instruct -e "Write a function that returns the nth

 Fibonacci number in Python."

 \`\`\`

 You’ll see the model start, generate a response, and then return to the

 prompt. If you get a “failed to bind” error again, make sure no other service

 is already listening on the default port (11434) – either stop the other

 service or change the port via OLLAMA\_HOST=0.0.0.0:11435 ollama serve.

 ──────────────────────────────────────────────────────────────────────────────

 3️⃣  Recommended pruning to stay within a reasonable disk budget

 ┌─────────────────────────────────────────────────┬──────────────────────────┐

 │ Keep                                            │ Reason                   │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ llama3.1:8b (4.9 GB)                            │ General‑purpose LLM –    │

 │                                                 │ core of your stack.      │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ phi4-mini:3.8b (2.5 GB)                         │ Strong 4‑bit compact     │

 │                                                 │ model – good fallback.   │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ qwen2.5-coder:1.5b-base (986 MB)                │ Small code model – keep  │

 │                                                 │ for generic coding.      │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ nomic-embed-text:latest (274 MB) or             │                          │

 │ bge‑small‑en (250 MB) – keep one.               │                          │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ mxbai-embed-large:latest (669 MB) – optional    │                          │

 │ (keep if you need higher‑quality embeddings).   │                          │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ Add qwen2.5:0.5b-instruct (≈ 400 MB) –          │                          │

 │ ultra‑tiny fallback.                            │                          │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ Add phi3:mini-4k-instruct (≈ 2 GB) – smaller    │                          │

 │ chat alternative to phi4‑mini.                  │                          │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ Add starcoder2:3b-code (≈ 2 GB) – dedicated     │                          │

 │ Python‑code model.                              │                          │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ Add tinyllama:1.1b-chat-v0.3 (≈ 1.2 GB) –       │                          │

 │ edge‑device chat.                               │                          │

 ├─────────────────────────────────────────────────┼──────────────────────────┤

 │ Add bge:small-en (≈ 250 MB) – higher‑quality    │                          │

 │ embed (replace Nomic if you prefer).            │                          │

 └─────────────────────────────────────────────────┴──────────────────────────┘

 Assuming you keep the above and drop everything else, the total disk usage is:

 \`\`\`

   4.9 GB (llama3.1)

   + 2.5 GB (phi4-mini)
   + 1.0 GB (qwen2.5‑coder)
   + 0.4 GB (qwen2.5‑0.5b‑instruct)
   + 2.0 GB (phi3-mini)
   + 2.0 GB (starcoder2‑code)
   + 1.2 GB (tinyllama)
   + 0.3 GB (bge‑small)
   + 0.7 GB (mxbai‑embed‑large – optional)

   ≈ 15 GB (≈ 13 GB without mxbai‑embed‑large)

 \`\`\`

 That fits comfortably on a 30 GB+ SSD while still giving you a well‑balanced

 toolbox (general, chat, code‑specialized, ultra‑tiny, and high‑quality

 embeddings).

 ──────────────────────────────────────────────────────────────────────────────

 4️⃣  How to decide which tiny model to run in a given environment

 ┌─────────────────────┬──────────────────────────────┬───────────────────────┐

 │ Environment         │ Recommended “tiny” model     │ Reason                │

 ├─────────────────────┼──────────────────────────────┼───────────────────────┤

 │ CPU‑only laptop     │ qwen2.5:0.5b-instruct or     │ < 1 GB RAM usage,     │

 │ with ≤ 8 GB RAM     │ tinyllama:1.1b-chat          │ sub‑second latency.   │

 ├─────────────────────┼──────────────────────────────┼───────────────────────┤

 │ CPU server with     │ phi3:mini-4k-instruct        │ Good chat quality,    │

 │ 16 GB RAM, want a   │ (≈ 2 GB)                     │ still under 4 GB      │

 │ chatbot but still   │                              │ total.                │

 │ stay light          │                              │                       │

 ├─────────────────────┼──────────────────────────────┼───────────────────────┤

 │ Edge device         │ tinyllama:1.1b-chat +        │ Both fit < 2 GB       │

 │ (Raspberry Pi,      │ bge:small‑en for embeddings  │ together.             │

 │ Jetson Nano)        │                              │                       │

 ├─────────────────────┼──────────────────────────────┼───────────────────────┤

 │ GPU‑accelerated     │ starcoder2:3b-code           │ GPU speeds the actual │

 │ workstation         │ (quantised q4\_k\_m) – runs in │ token generation      │

 │ (8‑12 GB VRAM)      │ ~2 GB VRAM, gives best       │ dramatically; 2 GB    │

 │                     │ Python code.                 │ VRAM is easy on a     │

 │                     │                              │ 8 GB card.            │

 ├─────────────────────┼──────────────────────────────┼───────────────────────┤

 │ Hybrid workflow     │ Keep phi4‑mini for chat,     │ Clean separation of   │

 │ (LLM for chat,      │ starcoder2‑code for Python,  │ responsibilities and  │

 │ separate code       │ qwen2.5‑0.5b‑instruct as a   │ you never exceed      │

 │ model)              │ cheap fallback.              │ memory limits.        │

 └─────────────────────┴──────────────────────────────┴───────────────────────┘

 ──────────────────────────────────────────────────────────────────────────────

 5️⃣  Quick copy‑paste commands to get all the new models in one go

 \`\`\`bash

   \# 1️⃣  Tiny & ultra‑tiny

   ollama pull qwen2.5:0.5b-instruct

   ollama pull phi3:mini-4k-instruct

   ollama pull tinyllama:1.1b-chat-v0.3

   \# 2️⃣  Code‑focused

   ollama pull starcoder2:3b-code

   \# If you also want the 7B variant (bigger, but still < 5 GB):

   \# ollama pull starcoder2:7b-code

   \# 3️⃣  Embedding upgrade

   ollama pull bge:small-en       # replaces Nomic‑embed‑text

   \# optional higher‑quality base:

   \# ollama pull bge:base-en

   \# 4️⃣  Optional 7‑B instruction model (pick ONE)

   ollama pull mistral:7b-instruct-v0.2   # ~4 GB

   \# or

   ollama pull gemma:2-9b-instruct       # ~5 GB

   \# 5️⃣  Optional Llama‑3.1‑Instruct (if you want the instruct variant)

   ollama pull llama3.1:8b-instruct

 \`\`\`

 If any of the ollama pull … commands fail because the model name is not yet in

 the public Ollama registry, just download the GGUF from Hugging Face and

 register it with the Modelfile approach described in §2.2.

 ──────────────────────────────────────────────────────────────────────────────

 6️⃣  Next steps for you

 1. Run the commands above (or pick the subset you need).
 2. Verify each model works:

    \`\`\`bash

      ollama run qwen2.5:0.5b-instruct -e "Explain the difference between list

    and tuple in Python."

    \`\`\`

 3. If you hit memory‑exhaustion errors, drop the largest model you don’t need

    (e.g., granite4.1:8b-q4\_K\_M or ornith-1.5:9b) – they’re both > 5 GB each

    and provide marginal benefit over Llama 3.1 8B+phi4‑mini combo.

 4. Update your “model inventory” (pi model list or ollama list) after you’ve

    removed the redundant ones.

 5. If you want a single unified repository (e.g., for a Docker‑based RAG or a

    local “model zoo”), export the list to a file:

    \`\`\`bash

      ollama list > ~/model\_inventory.txt

    \`\`\`

    Then you can feed that file into your deployment scripts.

 ──────────────────────────────────────────────────────────────────────────────

 \### TL;DR Recommended Additions

 ┌───────────────────────────────────┬───────┬────────────────────────────────┐

 │ Model                             │ Size  │ Use‑case                       │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ StarCoder 2 3B‑code               │ ~2 GB │ Dedicated Python/code          │

 │                                   │       │ generation                     │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ Qwen2.5 0.5B‑Instruct             │ ~400  │ Ultra‑tiny fallback for any    │

 │                                   │ MB    │ task                           │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ Phi‑3‑mini‑4k‑Instruct            │ ~2 GB │ Small but high‑quality         │

 │                                   │       │ chat/completion                │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ TinyLlama 1.1B‑Chat               │ ~1.2  │ Edge‑device chat               │

 │                                   │ GB    │                                │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ bge‑small‑en‑v1.5                 │ ~250  │ Better universal embedding     │

 │                                   │ MB    │ (replace Nomic)                │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ Mistral‑7B‑Instruct‑v0.2 (or      │ ~4‑5  │ Powerful 7‑9 B instruction     │

 │ Gemma‑2‑9B‑Instruct)              │ GB    │ model as an alternative to 8 B │

 │                                   │       │ Llama                          │

 ├───────────────────────────────────┼───────┼────────────────────────────────┤

 │ Meta‑Llama‑3.1‑8B‑Instruct        │ ~5 GB │ Instruction‑tuned 8 B LLM      │

 │                                   │       │ (upgrade from base Llama 3.1)  │

 └───────────────────────────────────┴───────┴────────────────────────────────┘

 Add these, prune the 5‑6 GB–plus “Ornith/Granite” giants you rarely use, and

 you’ll have a lean, high‑coverage toolkit that covers:

 - General chat (phi4‑mini / phi3-mini / tinyllama)
 - High‑quality Python coding (starcoder2‑code / codellama‑python)
 - Tiny universal fallback (qwen2.5‑0.5b)
 - Best‑in‑class embeddings (bge‑small or bge‑base)
 - Scalable 7‑9 B instruction (mistral‑7b‑instruct / gemma‑2‑9b‑instruct)
