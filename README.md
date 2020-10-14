# QuickBERTInference

## write_mask_preds/write_mask_preds.py Script

### For running the forward pass and saving replacements to file run the following command with the additional optional arguments:
This script needs to to be ran from inside the `write_mask_preds` folder, to be consistent with running using the Dockerfile on Beaker.

```
python write_mask_preds.py --data_dir ../../datasets/wiki-ann/wiki-ann/ --starts_with wiki --out_dir ../../datasets/processed_for_WSI/wiki/wiki000/replacements --dataset wiki --max_tokens_per_batch 16384 --fp16 --files_range 100-109
```

`max_tokens_per_batch=16384` is the max power of 2 that fits in a single P-100 GPU.

#### Mentionable Optional Arguments

`--iterativly_go_over_matrices`: An alternative method for going over predicted tokens and writing to disk. This is less optimized for PyTorch. Deprecated.

`--cpu`: Run on CPU, requires only when running on a machine with GPUs.

`--simple_sampler`: For a basic sampler (If using this, remove `max_tokens_per_batch` and choose a `batch_size` that fits your GPU).

`--fp16`: Running with half precision. Using `opt_level=O2`.

`--starts_with`: file starts with string.

`--files_range`: important for datasets with a lot of files where I want to split it between processes.

## analyze.py Script

This is accessed from `wsi_at_scale_streamlit.py`

## wsi_at_scale_streamlit.py Script

Run by `streamlit run wsi_at_scale_streamlit.py`

# Quick Access For debugging
```
from transformers import AutoTokenizer; model_hg_path = 'bert-large-uncased'; tokenizer = AutoTokenizer.from_pretrained(model_hg_path, use_fast=True)
t = ...
tokenizer.decode([])
```