# LLM_Wiki
This is just a place for us to put whatever we’ve learnt about LLMs, be it papers, blog posts or our own experiences.


## Overview
- [General Knowledge](https://github.com/krai/LLM_Wiki#general-knowledge)
- [Inference](https://github.com/krai/LLM_Wiki#inference)
- [Fine Tuning](https://github.com/krai/LLM_Wiki#fine-tuning)
- [Libraries](https://github.com/krai/LLM_Wiki#libraries)
- [Papers](https://github.com/krai/LLM_Wiki#paper)

## General Knowledge
- GBNF - A feature included in llama.cpp that allows you to control the output format of an LLM. It works by restricting the LLM’s output at each decode step, using a formal grammar. At the decode step, the LLM produces a probability distribution over the possible output tokens, for example {“a”: 0.25, “b”: 0.5, “c”: 0.25}, GBNF would then check which of these tokens is legal according to its grammar, and then readjust the probabilities - if “a” is an illegal token then the probability distribution becomes {“a”: 0, “b”: 0.67, “c”: 0.33”}. Now the only tokens that the LLM can output are ones that are legal according to the grammar. Note: I can only find this implemented in llama.cpp - not sure why.

## Inference

## Fine Tuning
Practical tips for fine-tuning LLMs

## Evaluation Metrics
- ROUGE - TODO 
- BLEU - TODO
- MAUVE - TODO
- LLM-as-a-Judge - Uses GPT4 to provide a score for some generated text. It can either generate a score for a single piece of text, or rank 2 pieces of text. Although it’s cool, it’s not a perfect metric, for example when ranking 2 pieces of text, GPT4 is more likely to prefer the first, regardless of the contents of the text.

## Libraries
- Llama.cpp - One of the first open source libraries built to allow people to run Facebook’s Llama, using its leaked weights. It’s mainly focused on Apple silicon but also has a CUDA backend.
- Huggingface Transformers - One of the most popular Python libraries for running transformer models.
- TensorRT-LLM

## Papers
- "Attention is all you need" - The original transformer paper, it’s not really that readable tho :(
- "LoRA: Low-Rank Adaptation of Large Language Models" - LoRA is a popular technique used to quickly finetune LLMs. It does this by attaching small “adapters” to the network which are updated during finetuning, whilst the original model weights are frozen. This blog post provides a good explanation with diagrams.
- "QLoRA: Efficient Finetuning of Quantized LLMs" - QLoRA is an even more efficient successor to LoRA, which trains the adapters using a quantized version of the model. They introduce a new data type (NF4) as well. Most importantly, they manage to finetune a 65B parameter model on a 48gb GPU in 24 hours, without sacrificing its (non-inference) performance.
- "AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration" - This is a smarter quantization strategy, which uses the activations of a model rather than its weights.
- "SLoRA: Federated Parameter Efficient Fine-Tuning of Language Models" - Not the actual S-LoRA.
- "S-LoRA - Serving Thousands of Concurrent LoRA Adapters" - This paper notices that if you have multiple fine-tuned LLMs, each using the same base model with LoRA, then you can improve inference performance by batching requests across LLMs as they share the base model. It also stores adapters in CPU memory, where they are paged in and out of GPU memory using their Unified Paging technique. They claim a 30x improvement in throughput over Huggingface Peft, but I think this might need to be verified, since HF doesn’t use a KV cache, nor does it have a default batching strategy.

## Glossary
