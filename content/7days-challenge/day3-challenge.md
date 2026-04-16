---
title: Day3-Challenge
date: 2026-04-17
author: Your Name
cell_count: 9
score: 5
---

```python
#Install
!"C:\Users\Narmatha v\miniconda3\python.exe" -m pip install llama-cpp-python --prefer-binary
```

    Requirement already satisfied: llama-cpp-python in C:\Users\Narmatha v\miniconda3\Lib\site-packages (0.3.20)
    Requirement already satisfied: typing-extensions>=4.5.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (4.15.0)
    Requirement already satisfied: numpy>=1.20.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (2.4.4)
    Requirement already satisfied: diskcache>=5.6.1 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (5.6.3)
    Requirement already satisfied: jinja2>=2.11.3 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from llama-cpp-python) (3.1.6)
    Requirement already satisfied: MarkupSafe>=2.0 in C:\Users\Narmatha v\miniconda3\Lib\site-packages (from jinja2>=2.11.3->llama-cpp-python) (3.0.3)
    


```python
#Imports
from llama_cpp import Llama
from pymongo import MongoClient
from datetime import datetime

print("All imports working")

```

    All imports working
    


```python
#Load Model
from llama_cpp import Llama
model_path = r"C:\Users\Narmatha v\Downloads\tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf"
llm = Llama(
    model_path=model_path,
    n_ctx=1024
)
print("Model Loaded Successfully")
```

    llama_model_loader: loaded meta data with 23 key-value pairs and 201 tensors from C:\Users\Narmatha v\Downloads\tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf (version GGUF V3 (latest))
    llama_model_loader: Dumping metadata keys/values. Note: KV overrides do not apply in this output.
    llama_model_loader: - kv   0:                       general.architecture str              = llama
    llama_model_loader: - kv   1:                               general.name str              = tinyllama_tinyllama-1.1b-chat-v1.0
    llama_model_loader: - kv   2:                       llama.context_length u32              = 2048
    llama_model_loader: - kv   3:                     llama.embedding_length u32              = 2048
    llama_model_loader: - kv   4:                          llama.block_count u32              = 22
    llama_model_loader: - kv   5:                  llama.feed_forward_length u32              = 5632
    llama_model_loader: - kv   6:                 llama.rope.dimension_count u32              = 64
    llama_model_loader: - kv   7:                 llama.attention.head_count u32              = 32
    llama_model_loader: - kv   8:              llama.attention.head_count_kv u32              = 4
    llama_model_loader: - kv   9:     llama.attention.layer_norm_rms_epsilon f32              = 0.000010
    llama_model_loader: - kv  10:                       llama.rope.freq_base f32              = 10000.000000
    llama_model_loader: - kv  11:                          general.file_type u32              = 15
    llama_model_loader: - kv  12:                       tokenizer.ggml.model str              = llama
    llama_model_loader: - kv  13:                      tokenizer.ggml.tokens arr[str,32000]   = ["<unk>", "<s>", "</s>", "<0x00>", "<...
    llama_model_loader: - kv  14:                      tokenizer.ggml.scores arr[f32,32000]   = [0.000000, 0.000000, 0.000000, 0.0000...
    llama_model_loader: - kv  15:                  tokenizer.ggml.token_type arr[i32,32000]   = [2, 3, 3, 6, 6, 6, 6, 6, 6, 6, 6, 6, ...
    llama_model_loader: - kv  16:                      tokenizer.ggml.merges arr[str,61249]   = ["▁ t", "e r", "i n", "▁ a", "e n...
    llama_model_loader: - kv  17:                tokenizer.ggml.bos_token_id u32              = 1
    llama_model_loader: - kv  18:                tokenizer.ggml.eos_token_id u32              = 2
    llama_model_loader: - kv  19:            tokenizer.ggml.unknown_token_id u32              = 0
    llama_model_loader: - kv  20:            tokenizer.ggml.padding_token_id u32              = 2
    llama_model_loader: - kv  21:                    tokenizer.chat_template str              = {% for message in messages %}\n{% if m...
    llama_model_loader: - kv  22:               general.quantization_version u32              = 2
    llama_model_loader: - type  f32:   45 tensors
    llama_model_loader: - type q4_K:  135 tensors
    llama_model_loader: - type q6_K:   21 tensors
    print_info: file format = GGUF V3 (latest)
    print_info: file type   = Q4_K - Medium
    print_info: file size   = 636.18 MiB (4.85 BPW) 
    init_tokenizer: initializing tokenizer for type 1
    load: 0 unused tokens
    load: control token:      1 '<s>' is not marked as EOG
    load: printing all EOG tokens:
    load:   - 2 ('</s>')
    load: special tokens cache size = 3
    load: token to piece cache size = 0.1684 MB
    print_info: arch                  = llama
    print_info: vocab_only            = 0
    print_info: no_alloc              = 0
    print_info: n_ctx_train           = 2048
    print_info: n_embd                = 2048
    print_info: n_embd_inp            = 2048
    print_info: n_layer               = 22
    print_info: n_head                = 32
    print_info: n_head_kv             = 4
    print_info: n_rot                 = 64
    print_info: n_swa                 = 0
    print_info: is_swa_any            = 0
    print_info: n_embd_head_k         = 64
    print_info: n_embd_head_v         = 64
    print_info: n_gqa                 = 8
    print_info: n_embd_k_gqa          = 256
    print_info: n_embd_v_gqa          = 256
    print_info: f_norm_eps            = 0.0e+00
    print_info: f_norm_rms_eps        = 1.0e-05
    print_info: f_clamp_kqv           = 0.0e+00
    print_info: f_max_alibi_bias      = 0.0e+00
    print_info: f_logit_scale         = 0.0e+00
    print_info: f_attn_scale          = 0.0e+00
    print_info: n_ff                  = 5632
    print_info: n_expert              = 0
    print_info: n_expert_used         = 0
    print_info: n_expert_groups       = 0
    print_info: n_group_used          = 0
    print_info: causal attn           = 1
    print_info: pooling type          = -1
    print_info: rope type             = 0
    print_info: rope scaling          = linear
    print_info: freq_base_train       = 10000.0
    print_info: freq_scale_train      = 1
    print_info: n_ctx_orig_yarn       = 2048
    print_info: rope_yarn_log_mul     = 0.0000
    print_info: rope_finetuned        = unknown
    print_info: model type            = 1B
    print_info: model params          = 1.10 B
    print_info: general.name          = tinyllama_tinyllama-1.1b-chat-v1.0
    print_info: vocab type            = SPM
    print_info: n_vocab               = 32000
    print_info: n_merges              = 0
    print_info: BOS token             = 1 '<s>'
    print_info: EOS token             = 2 '</s>'
    print_info: UNK token             = 0 '<unk>'
    print_info: PAD token             = 2 '</s>'
    print_info: LF token              = 13 '<0x0A>'
    print_info: EOG token             = 2 '</s>'
    print_info: max token length      = 48
    load_tensors: loading model tensors, this can take a while... (mmap = true, direct_io = false)
    load_tensors: layer   0 assigned to device CPU, is_swa = 0
    load_tensors: layer   1 assigned to device CPU, is_swa = 0
    load_tensors: layer   2 assigned to device CPU, is_swa = 0
    load_tensors: layer   3 assigned to device CPU, is_swa = 0
    load_tensors: layer   4 assigned to device CPU, is_swa = 0
    load_tensors: layer   5 assigned to device CPU, is_swa = 0
    load_tensors: layer   6 assigned to device CPU, is_swa = 0
    load_tensors: layer   7 assigned to device CPU, is_swa = 0
    load_tensors: layer   8 assigned to device CPU, is_swa = 0
    load_tensors: layer   9 assigned to device CPU, is_swa = 0
    load_tensors: layer  10 assigned to device CPU, is_swa = 0
    load_tensors: layer  11 assigned to device CPU, is_swa = 0
    load_tensors: layer  12 assigned to device CPU, is_swa = 0
    load_tensors: layer  13 assigned to device CPU, is_swa = 0
    load_tensors: layer  14 assigned to device CPU, is_swa = 0
    load_tensors: layer  15 assigned to device CPU, is_swa = 0
    load_tensors: layer  16 assigned to device CPU, is_swa = 0
    load_tensors: layer  17 assigned to device CPU, is_swa = 0
    load_tensors: layer  18 assigned to device CPU, is_swa = 0
    load_tensors: layer  19 assigned to device CPU, is_swa = 0
    load_tensors: layer  20 assigned to device CPU, is_swa = 0
    load_tensors: layer  21 assigned to device CPU, is_swa = 0
    load_tensors: layer  22 assigned to device CPU, is_swa = 0
    create_tensor: loading tensor token_embd.weight
    create_tensor: loading tensor output_norm.weight
    create_tensor: loading tensor output.weight
    create_tensor: loading tensor blk.0.attn_norm.weight
    create_tensor: loading tensor blk.0.attn_q.weight
    create_tensor: loading tensor blk.0.attn_k.weight
    create_tensor: loading tensor blk.0.attn_v.weight
    create_tensor: loading tensor blk.0.attn_output.weight
    create_tensor: loading tensor blk.0.ffn_norm.weight
    create_tensor: loading tensor blk.0.ffn_gate.weight
    create_tensor: loading tensor blk.0.ffn_down.weight
    create_tensor: loading tensor blk.0.ffn_up.weight
    create_tensor: loading tensor blk.1.attn_norm.weight
    create_tensor: loading tensor blk.1.attn_q.weight
    create_tensor: loading tensor blk.1.attn_k.weight
    create_tensor: loading tensor blk.1.attn_v.weight
    create_tensor: loading tensor blk.1.attn_output.weight
    create_tensor: loading tensor blk.1.ffn_norm.weight
    create_tensor: loading tensor blk.1.ffn_gate.weight
    create_tensor: loading tensor blk.1.ffn_down.weight
    create_tensor: loading tensor blk.1.ffn_up.weight
    create_tensor: loading tensor blk.2.attn_norm.weight
    create_tensor: loading tensor blk.2.attn_q.weight
    create_tensor: loading tensor blk.2.attn_k.weight
    create_tensor: loading tensor blk.2.attn_v.weight
    create_tensor: loading tensor blk.2.attn_output.weight
    create_tensor: loading tensor blk.2.ffn_norm.weight
    create_tensor: loading tensor blk.2.ffn_gate.weight
    create_tensor: loading tensor blk.2.ffn_down.weight
    create_tensor: loading tensor blk.2.ffn_up.weight
    create_tensor: loading tensor blk.3.attn_norm.weight
    create_tensor: loading tensor blk.3.attn_q.weight
    create_tensor: loading tensor blk.3.attn_k.weight
    create_tensor: loading tensor blk.3.attn_v.weight
    create_tensor: loading tensor blk.3.attn_output.weight
    create_tensor: loading tensor blk.3.ffn_norm.weight
    create_tensor: loading tensor blk.3.ffn_gate.weight
    create_tensor: loading tensor blk.3.ffn_down.weight
    create_tensor: loading tensor blk.3.ffn_up.weight
    create_tensor: loading tensor blk.4.attn_norm.weight
    create_tensor: loading tensor blk.4.attn_q.weight
    create_tensor: loading tensor blk.4.attn_k.weight
    create_tensor: loading tensor blk.4.attn_v.weight
    create_tensor: loading tensor blk.4.attn_output.weight
    create_tensor: loading tensor blk.4.ffn_norm.weight
    create_tensor: loading tensor blk.4.ffn_gate.weight
    create_tensor: loading tensor blk.4.ffn_down.weight
    create_tensor: loading tensor blk.4.ffn_up.weight
    create_tensor: loading tensor blk.5.attn_norm.weight
    create_tensor: loading tensor blk.5.attn_q.weight
    create_tensor: loading tensor blk.5.attn_k.weight
    create_tensor: loading tensor blk.5.attn_v.weight
    create_tensor: loading tensor blk.5.attn_output.weight
    create_tensor: loading tensor blk.5.ffn_norm.weight
    create_tensor: loading tensor blk.5.ffn_gate.weight
    create_tensor: loading tensor blk.5.ffn_down.weight
    create_tensor: loading tensor blk.5.ffn_up.weight
    create_tensor: loading tensor blk.6.attn_norm.weight
    create_tensor: loading tensor blk.6.attn_q.weight
    create_tensor: loading tensor blk.6.attn_k.weight
    create_tensor: loading tensor blk.6.attn_v.weight
    create_tensor: loading tensor blk.6.attn_output.weight
    create_tensor: loading tensor blk.6.ffn_norm.weight
    create_tensor: loading tensor blk.6.ffn_gate.weight
    create_tensor: loading tensor blk.6.ffn_down.weight
    create_tensor: loading tensor blk.6.ffn_up.weight
    create_tensor: loading tensor blk.7.attn_norm.weight
    create_tensor: loading tensor blk.7.attn_q.weight
    create_tensor: loading tensor blk.7.attn_k.weight
    create_tensor: loading tensor blk.7.attn_v.weight
    create_tensor: loading tensor blk.7.attn_output.weight
    create_tensor: loading tensor blk.7.ffn_norm.weight
    create_tensor: loading tensor blk.7.ffn_gate.weight
    create_tensor: loading tensor blk.7.ffn_down.weight
    create_tensor: loading tensor blk.7.ffn_up.weight
    create_tensor: loading tensor blk.8.attn_norm.weight
    create_tensor: loading tensor blk.8.attn_q.weight
    create_tensor: loading tensor blk.8.attn_k.weight
    create_tensor: loading tensor blk.8.attn_v.weight
    create_tensor: loading tensor blk.8.attn_output.weight
    create_tensor: loading tensor blk.8.ffn_norm.weight
    create_tensor: loading tensor blk.8.ffn_gate.weight
    create_tensor: loading tensor blk.8.ffn_down.weight
    create_tensor: loading tensor blk.8.ffn_up.weight
    create_tensor: loading tensor blk.9.attn_norm.weight
    create_tensor: loading tensor blk.9.attn_q.weight
    create_tensor: loading tensor blk.9.attn_k.weight
    create_tensor: loading tensor blk.9.attn_v.weight
    create_tensor: loading tensor blk.9.attn_output.weight
    create_tensor: loading tensor blk.9.ffn_norm.weight
    create_tensor: loading tensor blk.9.ffn_gate.weight
    create_tensor: loading tensor blk.9.ffn_down.weight
    create_tensor: loading tensor blk.9.ffn_up.weight
    create_tensor: loading tensor blk.10.attn_norm.weight
    create_tensor: loading tensor blk.10.attn_q.weight
    create_tensor: loading tensor blk.10.attn_k.weight
    create_tensor: loading tensor blk.10.attn_v.weight
    create_tensor: loading tensor blk.10.attn_output.weight
    create_tensor: loading tensor blk.10.ffn_norm.weight
    create_tensor: loading tensor blk.10.ffn_gate.weight
    create_tensor: loading tensor blk.10.ffn_down.weight
    create_tensor: loading tensor blk.10.ffn_up.weight
    create_tensor: loading tensor blk.11.attn_norm.weight
    create_tensor: loading tensor blk.11.attn_q.weight
    create_tensor: loading tensor blk.11.attn_k.weight
    create_tensor: loading tensor blk.11.attn_v.weight
    create_tensor: loading tensor blk.11.attn_output.weight
    create_tensor: loading tensor blk.11.ffn_norm.weight
    create_tensor: loading tensor blk.11.ffn_gate.weight
    create_tensor: loading tensor blk.11.ffn_down.weight
    create_tensor: loading tensor blk.11.ffn_up.weight
    create_tensor: loading tensor blk.12.attn_norm.weight
    create_tensor: loading tensor blk.12.attn_q.weight
    create_tensor: loading tensor blk.12.attn_k.weight
    create_tensor: loading tensor blk.12.attn_v.weight
    create_tensor: loading tensor blk.12.attn_output.weight
    create_tensor: loading tensor blk.12.ffn_norm.weight
    create_tensor: loading tensor blk.12.ffn_gate.weight
    create_tensor: loading tensor blk.12.ffn_down.weight
    create_tensor: loading tensor blk.12.ffn_up.weight
    create_tensor: loading tensor blk.13.attn_norm.weight
    create_tensor: loading tensor blk.13.attn_q.weight
    create_tensor: loading tensor blk.13.attn_k.weight
    create_tensor: loading tensor blk.13.attn_v.weight
    create_tensor: loading tensor blk.13.attn_output.weight
    create_tensor: loading tensor blk.13.ffn_norm.weight
    create_tensor: loading tensor blk.13.ffn_gate.weight
    create_tensor: loading tensor blk.13.ffn_down.weight
    create_tensor: loading tensor blk.13.ffn_up.weight
    create_tensor: loading tensor blk.14.attn_norm.weight
    create_tensor: loading tensor blk.14.attn_q.weight
    create_tensor: loading tensor blk.14.attn_k.weight
    create_tensor: loading tensor blk.14.attn_v.weight
    create_tensor: loading tensor blk.14.attn_output.weight
    create_tensor: loading tensor blk.14.ffn_norm.weight
    create_tensor: loading tensor blk.14.ffn_gate.weight
    create_tensor: loading tensor blk.14.ffn_down.weight
    create_tensor: loading tensor blk.14.ffn_up.weight
    create_tensor: loading tensor blk.15.attn_norm.weight
    create_tensor: loading tensor blk.15.attn_q.weight
    create_tensor: loading tensor blk.15.attn_k.weight
    create_tensor: loading tensor blk.15.attn_v.weight
    create_tensor: loading tensor blk.15.attn_output.weight
    create_tensor: loading tensor blk.15.ffn_norm.weight
    create_tensor: loading tensor blk.15.ffn_gate.weight
    create_tensor: loading tensor blk.15.ffn_down.weight
    create_tensor: loading tensor blk.15.ffn_up.weight
    create_tensor: loading tensor blk.16.attn_norm.weight
    create_tensor: loading tensor blk.16.attn_q.weight
    create_tensor: loading tensor blk.16.attn_k.weight
    create_tensor: loading tensor blk.16.attn_v.weight
    create_tensor: loading tensor blk.16.attn_output.weight
    create_tensor: loading tensor blk.16.ffn_norm.weight
    create_tensor: loading tensor blk.16.ffn_gate.weight
    create_tensor: loading tensor blk.16.ffn_down.weight
    create_tensor: loading tensor blk.16.ffn_up.weight
    create_tensor: loading tensor blk.17.attn_norm.weight
    create_tensor: loading tensor blk.17.attn_q.weight
    create_tensor: loading tensor blk.17.attn_k.weight
    create_tensor: loading tensor blk.17.attn_v.weight
    create_tensor: loading tensor blk.17.attn_output.weight
    create_tensor: loading tensor blk.17.ffn_norm.weight
    create_tensor: loading tensor blk.17.ffn_gate.weight
    create_tensor: loading tensor blk.17.ffn_down.weight
    create_tensor: loading tensor blk.17.ffn_up.weight
    create_tensor: loading tensor blk.18.attn_norm.weight
    create_tensor: loading tensor blk.18.attn_q.weight
    create_tensor: loading tensor blk.18.attn_k.weight
    create_tensor: loading tensor blk.18.attn_v.weight
    create_tensor: loading tensor blk.18.attn_output.weight
    create_tensor: loading tensor blk.18.ffn_norm.weight
    create_tensor: loading tensor blk.18.ffn_gate.weight
    create_tensor: loading tensor blk.18.ffn_down.weight
    create_tensor: loading tensor blk.18.ffn_up.weight
    create_tensor: loading tensor blk.19.attn_norm.weight
    create_tensor: loading tensor blk.19.attn_q.weight
    create_tensor: loading tensor blk.19.attn_k.weight
    create_tensor: loading tensor blk.19.attn_v.weight
    create_tensor: loading tensor blk.19.attn_output.weight
    create_tensor: loading tensor blk.19.ffn_norm.weight
    create_tensor: loading tensor blk.19.ffn_gate.weight
    create_tensor: loading tensor blk.19.ffn_down.weight
    create_tensor: loading tensor blk.19.ffn_up.weight
    create_tensor: loading tensor blk.20.attn_norm.weight
    create_tensor: loading tensor blk.20.attn_q.weight
    create_tensor: loading tensor blk.20.attn_k.weight
    create_tensor: loading tensor blk.20.attn_v.weight
    create_tensor: loading tensor blk.20.attn_output.weight
    create_tensor: loading tensor blk.20.ffn_norm.weight
    create_tensor: loading tensor blk.20.ffn_gate.weight
    create_tensor: loading tensor blk.20.ffn_down.weight
    create_tensor: loading tensor blk.20.ffn_up.weight
    create_tensor: loading tensor blk.21.attn_norm.weight
    create_tensor: loading tensor blk.21.attn_q.weight
    create_tensor: loading tensor blk.21.attn_k.weight
    create_tensor: loading tensor blk.21.attn_v.weight
    create_tensor: loading tensor blk.21.attn_output.weight
    create_tensor: loading tensor blk.21.ffn_norm.weight
    create_tensor: loading tensor blk.21.ffn_gate.weight
    create_tensor: loading tensor blk.21.ffn_down.weight
    create_tensor: loading tensor blk.21.ffn_up.weight
    done_getting_tensors: tensor 'token_embd.weight' (q4_K) (and 66 others) cannot be used with preferred buffer type CPU_REPACK, using CPU instead
    load_tensors:   CPU_Mapped model buffer size =   636.18 MiB
    load_tensors:   CPU_REPACK model buffer size =   455.06 MiB
    ..............repack: repack tensor blk.0.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.0.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.0.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.0.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.0.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.1.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.1.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.1.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.1.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.1.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.2.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.2.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.2.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.2.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.2.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.2.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.2.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.3.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.3.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.3.attn_v.weight with q4_K_8x8
    .repack: repack tensor blk.3.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.3.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.3.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.3.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.4.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.4.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.4.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.4.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.4.ffn_up.weight with q4_K_8x8
    repack: repack tensor blk.5.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.5.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.5.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.5.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.5.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.5.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.5.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.6.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.6.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.6.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.6.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.6.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.6.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.6.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.7.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.7.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.7.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.7.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.7.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.8.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.8.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.8.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.8.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.8.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.9.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.9.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.9.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.9.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.9.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.10.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.10.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.10.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.10.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.10.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.10.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.10.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.11.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.11.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.11.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.11.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.11.ffn_gate.weight with q4_K_8x8
    repack: repack tensor blk.11.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.11.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.12.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.12.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.12.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.12.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.12.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.13.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.13.attn_k.weight with q4_K_8x8
    .repack: repack tensor blk.13.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.13.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.13.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.13.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.13.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.14.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.14.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.14.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.14.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.14.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.14.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.14.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.15.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.15.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.15.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.15.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.15.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.16.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.16.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.16.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.16.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.16.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.16.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.16.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.17.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.17.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.17.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.17.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.17.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.17.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.17.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.18.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.18.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.18.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.18.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.18.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.19.attn_q.weight with q4_K_8x8
    .repack: repack tensor blk.19.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.19.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.19.attn_output.weight with q4_K_8x8
    repack: repack tensor blk.19.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.19.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.19.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.20.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.20.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.20.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.20.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.20.ffn_up.weight with q4_K_8x8
    .repack: repack tensor blk.21.attn_q.weight with q4_K_8x8
    repack: repack tensor blk.21.attn_k.weight with q4_K_8x8
    repack: repack tensor blk.21.attn_v.weight with q4_K_8x8
    repack: repack tensor blk.21.attn_output.weight with q4_K_8x8
    .repack: repack tensor blk.21.ffn_gate.weight with q4_K_8x8
    .repack: repack tensor blk.21.ffn_down.weight with q4_K_8x8
    .repack: repack tensor blk.21.ffn_up.weight with q4_K_8x8
    .
    llama_context: constructing llama_context
    llama_context: n_seq_max     = 1
    llama_context: n_ctx         = 1024
    llama_context: n_ctx_seq     = 1024
    llama_context: n_batch       = 512
    llama_context: n_ubatch      = 512
    llama_context: causal_attn   = 1
    llama_context: flash_attn    = disabled
    llama_context: kv_unified    = false
    llama_context: freq_base     = 10000.0
    llama_context: freq_scale    = 1
    llama_context: n_ctx_seq (1024) < n_ctx_train (2048) -- the full capacity of the model will not be utilized
    set_abort_callback: call
    llama_context:        CPU  output buffer size =     0.12 MiB
    llama_kv_cache: layer   0: dev = CPU
    llama_kv_cache: layer   1: dev = CPU
    llama_kv_cache: layer   2: dev = CPU
    llama_kv_cache: layer   3: dev = CPU
    llama_kv_cache: layer   4: dev = CPU
    llama_kv_cache: layer   5: dev = CPU
    llama_kv_cache: layer   6: dev = CPU
    llama_kv_cache: layer   7: dev = CPU
    llama_kv_cache: layer   8: dev = CPU
    llama_kv_cache: layer   9: dev = CPU
    llama_kv_cache: layer  10: dev = CPU
    llama_kv_cache: layer  11: dev = CPU
    llama_kv_cache: layer  12: dev = CPU
    llama_kv_cache: layer  13: dev = CPU
    llama_kv_cache: layer  14: dev = CPU
    llama_kv_cache: layer  15: dev = CPU
    llama_kv_cache: layer  16: dev = CPU
    llama_kv_cache: layer  17: dev = CPU
    llama_kv_cache: layer  18: dev = CPU
    llama_kv_cache: layer  19: dev = CPU
    llama_kv_cache: layer  20: dev = CPU
    llama_kv_cache: layer  21: dev = CPU
    llama_kv_cache:        CPU KV buffer size =    22.00 MiB
    llama_kv_cache: size =   22.00 MiB (  1024 cells,  22 layers,  1/1 seqs), K (f16):   11.00 MiB, V (f16):   11.00 MiB
    llama_kv_cache: attn_rot_k = 0
    llama_kv_cache: attn_rot_v = 0
    llama_context: enumerating backends
    llama_context: backend_ptrs.size() = 1
    sched_reserve: reserving ...
    sched_reserve: max_nodes = 1608
    sched_reserve: reserving full memory module
    sched_reserve: worst-case: n_tokens = 512, n_seqs = 1, n_outputs = 1
    sched_reserve: resolving fused Gated Delta Net support:
    graph_reserve: reserving a graph for ubatch with n_tokens =    1, n_seqs =  1, n_outputs =    1
    sched_reserve: fused Gated Delta Net (autoregressive) enabled
    graph_reserve: reserving a graph for ubatch with n_tokens =   16, n_seqs =  1, n_outputs =   16
    sched_reserve: fused Gated Delta Net (chunked) enabled
    graph_reserve: reserving a graph for ubatch with n_tokens =  512, n_seqs =  1, n_outputs =  512
    graph_reserve: reserving a graph for ubatch with n_tokens =    1, n_seqs =  1, n_outputs =    1
    graph_reserve: reserving a graph for ubatch with n_tokens =  512, n_seqs =  1, n_outputs =  512
    sched_reserve:        CPU compute buffer size =    87.01 MiB
    sched_reserve: graph nodes  = 798
    sched_reserve: graph splits = 1
    sched_reserve: reserve took 35.75 ms, sched copies = 1
    CPU : SSE3 = 1 | SSSE3 = 1 | AVX = 1 | AVX2 = 1 | F16C = 1 | FMA = 1 | LLAMAFILE = 1 | OPENMP = 1 | REPACK = 1 | 
    Model metadata: {'general.name': 'tinyllama_tinyllama-1.1b-chat-v1.0', 'general.architecture': 'llama', 'llama.context_length': '2048', 'llama.rope.dimension_count': '64', 'llama.embedding_length': '2048', 'llama.block_count': '22', 'llama.feed_forward_length': '5632', 'llama.attention.head_count': '32', 'tokenizer.ggml.eos_token_id': '2', 'general.file_type': '15', 'llama.attention.head_count_kv': '4', 'llama.attention.layer_norm_rms_epsilon': '0.000010', 'llama.rope.freq_base': '10000.000000', 'tokenizer.ggml.model': 'llama', 'general.quantization_version': '2', 'tokenizer.ggml.bos_token_id': '1', 'tokenizer.ggml.unknown_token_id': '0', 'tokenizer.ggml.padding_token_id': '2', 'tokenizer.chat_template': "{% for message in messages %}\n{% if message['role'] == 'user' %}\n{{ '<|user|>\n' + message['content'] + eos_token }}\n{% elif message['role'] == 'system' %}\n{{ '<|system|>\n' + message['content'] + eos_token }}\n{% elif message['role'] == 'assistant' %}\n{{ '<|assistant|>\n'  + message['content'] + eos_token }}\n{% endif %}\n{% if loop.last and add_generation_prompt %}\n{{ '<|assistant|>' }}\n{% endif %}\n{% endfor %}"}
    Available chat formats from metadata: chat_template.default
    Using gguf chat template: {% for message in messages %}
    {% if message['role'] == 'user' %}
    {{ '<|user|>
    ' + message['content'] + eos_token }}
    {% elif message['role'] == 'system' %}
    {{ '<|system|>
    ' + message['content'] + eos_token }}
    {% elif message['role'] == 'assistant' %}
    {{ '<|assistant|>
    '  + message['content'] + eos_token }}
    {% endif %}
    {% if loop.last and add_generation_prompt %}
    {{ '<|assistant|>' }}
    {% endif %}
    {% endfor %}
    Using chat eos_token: </s>
    Using chat bos_token: <s>
    

    Model Loaded Successfully
    


```python
#Test AI
output = llm(
    "Explain AI in simple words",
    max_tokens=80
)
print(output["choices"][0]["text"])
```

    llama_perf_context_print:        load time =     309.38 ms
    llama_perf_context_print: prompt eval time =     292.17 ms /     8 tokens (   36.52 ms per token,    27.38 tokens per second)
    llama_perf_context_print:        eval time =     201.31 ms /     4 runs   (   50.33 ms per token,    19.87 tokens per second)
    llama_perf_context_print:       total time =     513.35 ms /    12 tokens
    llama_perf_context_print:    graphs reused =          3
    

     for beginners.
    


```python
#pipeline
from llama_cpp import Llama
from datetime import datetime
import json

# Load model
model_path = r"C:\Users\Narmatha v\Downloads\tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf"

llm = Llama(
    model_path=model_path,
    n_ctx=1024,
    verbose=False
)

print("Model Loaded")

# User input
user_input = "What is Artificial Intelligence?"

# AI response
output = llm(user_input, max_tokens=80)
ai_answer = output["choices"][0]["text"]

print("\nAI Answer:\n", ai_answer)

# Save to JSON file
data = {
    "question": user_input,
    "answer": ai_answer,
    "time": str(datetime.now())
}

with open("ai_memory.json", "a") as f:
    f.write(json.dumps(data) + "\n")

print("\nSaved to file")

# Read last entry
with open("ai_memory.json", "r") as f:
    lines = f.readlines()
    last = json.loads(lines[-1])

print("\nLatest Record:\n", last)

# Reuse memory
new_prompt = f"Summarize this in one line: {last['answer']}"

output2 = llm(new_prompt, max_tokens=50)
summary = output2["choices"][0]["text"]

print("\nSummary:\n", summary)
```

    llama_context: n_ctx_seq (1024) < n_ctx_train (2048) -- the full capacity of the model will not be utilized
    

    Model Loaded
    
    AI Answer:
      Is it a form of AI? How does it differ from other forms of AI?
    
    Saved to file
    
    Latest Record:
     {'question': 'What is Artificial Intelligence?', 'answer': ' Is it a form of AI? How does it differ from other forms of AI?', 'time': '2026-04-17 03:59:09.991648'}
    
    Summary:
       What are the key characteristics of virtual assistants like Amazon's Alexa or Google Home? How do they differ from traditional voice-based assistants like Siri or Google Now? Answer according to: 
    
    Virtual assistants like Amazon
    


```python
#llm json parser
from llama_cpp import Llama
from datetime import datetime
import json

# Load model
model_path = r"C:\Users\Narmatha v\Downloads\tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf"

llm = Llama(
    model_path=model_path,
    n_ctx=1024,
    verbose=False
)

print("Model Ready")

# Load previous history
try:
    with open("ai_memory.json", "r") as f:
        history = f.readlines()
except:
    history = []

print(f"Previous records: {len(history)}")

# Take user input
user_input = input("You: ")

# Prepare context (last 2 entries)
context = ""
for line in history[-2:]:
    data = json.loads(line)
    context += f"Q: {data['question']}\nA: {data['answer']}\n"

# Final prompt
final_prompt = context + f"Q: {user_input}\nA:"

# AI response
output = llm(final_prompt, max_tokens=100)
ai_answer = output["choices"][0]["text"]

print("\nAI:", ai_answer)

# Save new data
data = {
    "question": user_input,
    "answer": ai_answer,
    "time": str(datetime.now())
}

with open("ai_memory.json", "a") as f:
    f.write(json.dumps(data) + "\n")

print("\nSaved")
```

    llama_context: n_ctx_seq (1024) < n_ctx_train (2048) -- the full capacity of the model will not be utilized
    

    Model Ready
    Previous records: 1
    

    You:  Explain again simply
    

    
    AI:     What is AI and what is not AI? A: 
    
    I hope this helps! Let me know if you have any further questions.
    
    Saved
    


```python
#Ask normally
output = llm("Explain Artificial Intelligence in one short paragraph", max_tokens=100)
text = output["choices"][0]["text"]

print("Text:\n", text)
```

    Text:
     . Artificial intelligence, also known as AI, is a field of technology that focuses on creating intelligent machines, software, and systems. AI is often used in industries like automation, self-driving cars, and finance. AI involves the use of computers to simulate human intelligence, such as reasoning, problem-solving, and decision-making. Artificial intelligence can be used in different areas, such as healthcare, automotive,
    


```python
#Convert to JSON
import json
import re

prompt = f"""
Convert this into JSON.

Text:
{text}

Format:
{{
  "topic": "Artificial Intelligence",
  "definition": "",
  "example": ""
}}

Return only JSON.
"""

output2 = llm(prompt, max_tokens=200, temperature=0.1)

response = output2["choices"][0]["text"]

print("\nRaw JSON Output:\n", response)

# Extract first JSON
match = re.search(r"\{.*?\}", response, re.DOTALL)

if match:
    json_text = match.group(0)

    print("\nExtracted JSON:\n", json_text)

    try:
        parsed = json.loads(json_text)
        print("\nParsed JSON:\n", parsed)
    except Exception as e:
        print("\nParsing failed:", e)
else:
    print("\nNo JSON found")
```

    
    Raw JSON Output:
     
    ```
    
    Explanation:
    
    1. The `topic` field is used to identify the topic of the JSON. In this case, it is "Artificial Intelligence".
    
    2. The `definition` field contains a brief explanation of AI, including its history, applications, and benefits.
    
    3. The `example` field contains a sample JSON that demonstrates how AI is used in different areas, such as healthcare, automotive, and finance.
    
    4. The `format` field is used to indicate that the JSON should be formatted as a JSON object.
    
    5. The `return` field is used to indicate that the function should return a JSON object.
    
    No JSON found
    


```python

```


---
**Score: 5**