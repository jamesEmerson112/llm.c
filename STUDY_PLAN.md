# LLM.c Study Plan (Simplified)

This guide is designed to help you understand `llm.c` without getting overwhelmed. Think of this project as a bare-bones education tool to learn how Large Language Models (LLMs) like GPT-2 work, using simple C code.

## 0. Can I run this? (Yes!)

**You do NOT need a Linux machine or a fancy NVIDIA Graphics Card (GPU) to learn from this.**

*   **Windows Users:** This project works on Windows.
*   **No GPU?** No problem. You can run the "CPU" versions. They are slower but perfect for learning and debugging.
*   **With GPU:** If you have an NVIDIA card, you can run the "CUDA" versions to train much faster.

## Phase 1: Hello World (CPU Only)

Goal: Get the model running on your computer using just the Central Processing Unit (CPU).

**Step 1: Get the Data**
Before training a model, it needs something to read. We use "TinyShakespeare" (a small collection of Shakespeare works).

Run this in your terminal:
```bash
python dev/data/tinyshakespeare.py
```
*   **What this does:** Downloads text and converts it into a "tokenized" format (numbers) that the computer can read, saving it as `.bin` files in `dev/data/tinyshakespeare/`.

**Step 2: The Python Reference (Optional but Recommended)**
First, run the PyTorch version. This is the "easy to read" reference written in Python.

```bash
python train_gpt2.py
```
*   **What to watch:** It will print the "loss" (error rate) going down. This confirms your data is ready and your Python setup is correct.

**Step 3: The C Implementation (The Real Deal)**
Now, let's run the same thing in pure C.

*   **Command:** `make train_gpt2`
*   **Run it:** `./train_gpt2` (or `train_gpt2.exe` on Windows)

*   **What this does:** It compiles `train_gpt2.c` and runs it. You should see similar "loss" numbers to the Python version. Congratulations! You just trained a mini-GPT-2 in C.

## Phase 2: Understanding the "Magic"

Goal: Understand how the code actually works.

**The Main Event: `train_gpt2.c`**
This single file contains almost everything. It is about ~1,000 lines of clean C code.

**Study Strategy:**
1.  **Open two windows side-by-side:**
    *   Left: `train_gpt2.py` (Python/PyTorch)
    *   Right: `train_gpt2.c` (Pure C)
2.  **Compare "Forward Pass":** Look at how the model predicts the next token.
    *   In Python, it's often one line (e.g., `self.transformer(x)`).
    *   In C, you'll see the loops that actually do the math (matrix multiplications).
3.  **Key Functions to look for in C:**
    *   `matmul_forward`: The heavy lifting (Matrix Multiplication).
    *   `attention_forward`: The "Attention" mechanism (how the model looks back at previous words).

## Phase 3: Level Up (GPU / CUDA) - *Optional*

Goal: Make it go fast.

If you have an NVIDIA GPU, you can try the CUDA version.

1.  **The File:** `train_gpt2.cu`
2.  **The Difference:** This file moves the math from the CPU to the GPU.
3.  **To Run:**
    ```bash
    make train_gpt2cu
    ./train_gpt2cu
    ```
4.  **Study Tip:** Compare `train_gpt2.c` (CPU) with `train_gpt2.cu` (GPU). You will see how simple loops in C become "Kernels" (parallel functions) in CUDA to run on thousands of GPU cores at once.

## Summary Checklist

1.  [ ] **Data:** Run `python dev/data/tinyshakespeare.py`
2.  [ ] **Run C:** Compile and run `train_gpt2.c`.
3.  [ ] **Read:** Read `train_gpt2.c` comments to understand the flow.
