# Google-Tunix-
Google Tunix hackathon 
Google Tunix Reasoning Hackathon - Complete Solution 
📋 Competition Summary
Goal: Train Google's Gemma model to show step-by-step reasoning for math problems

🎯 Solution Strategy
Phase 1: Data Preparation (Day 1-2)
Recommended Datasets:

GSM8K - Grade school math (8.5K problems)
MATH - Competition math problems
MetaMathQA - 400K math Q&A pairs
MathInstruct - Diverse math reasoning
Data Format:

<reasoning>
Question: [problem statement]

Let me think through this step-by-step:
[step 1 explanation]
[step 2 explanation]
...

Therefore, the answer is: [final answer]
</reasoning>
Phase 2: Model Setup (Day 3-4)
Model Choice:

Gemma2 2B (recommended) - Better balance of performance and speed
Gemma3 1B - Faster training, less capable
Training Approach:

LoRA (Low-Rank Adaptation) - Memory efficient fine-tuning
QLoRA - Quantized LoRA for even better efficiency
Parameters:
LoRA rank (r): 16-32
LoRA alpha: 32-64
Target modules: attention layers (q_proj, k_proj, v_proj, o_proj)
Phase 3: Training (Day 5-8)
Hyperparameters:

python
learning_rate: 2e-4
batch_size: 4 (with gradient accumulation)
epochs: 3-5
warmup_steps: 100-200
max_seq_length: 512-1024
gradient_checkpointing: True
bf16: True (for TPU)
Training Strategy:

Start with smaller dataset (GSM8K) to validate pipeline
Expand to larger datasets if time permits
Use curriculum learning: simple → complex problems
Monitor loss and sample generations regularly
TPU Optimization:

Use bf16 precision (not fp16)
Enable gradient checkpointing
Use gradient accumulation for effective larger batch sizes
Save checkpoints frequently (TPU time is limited)
Phase 4: Evaluation & Iteration (Day 9-10)
Test Your Model:

python
test_questions = [
    "If x + 5 = 12, what is x?",
    "Calculate 15% of 80",
    "A train travels 60 km/h for 2.5 hours. What distance did it cover?"
]
Evaluation Metrics:

Reasoning quality: Are steps logical and correct?
Final answer accuracy: Is the answer correct?
Format compliance: Does output follow required format?
