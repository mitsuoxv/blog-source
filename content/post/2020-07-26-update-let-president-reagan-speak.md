---
title: 'Update: let President Reagan speak'
author: Mitsuo Shiota
date: '2020-07-26'
slug: update-let-president-reagan-speak
categories:
  - economics
tags:
  - Python
  - tensorflow
---

## OpenAI's GPT-2 model

In June 2020, OpenAI released GPT-3, a new text generator. Its reputation is very high. However, I can't try it, because its size with 175 billion parameters is huge, and I can't access [OpenAI API](https://openai.com/blog/openai-api/).

So I looked around for information about an old one, GPT-2. I found [gpt-2-simple module by Max Woolf](https://github.com/minimaxir/gpt-2-simple), and decided to try it.

## I use reports from 1982 to 1989 by President Reagan

I combined reports from 1982 to 1989 into reagan.txt.

## I tried docker, but failed due to ResourceExhaustedError

As gpt-2-simple module requires tensorflow 1.14 or 15, I create docker like below.

```
docker run -u $(id -u):$(id -g) \
  --gpus all -it -p 8888:8888 -v `pwd`:/tf/notebooks \
  tensorflow/tensorflow:1.15.2-gpu-py3-jupyter
```

I tried the smallest model, "124M", in [gpt-2-try-and-error.ipynb](https://github.com/mitsuoxv/erp/blob/master/gpt-2-try-and-error.ipynb), but failed due to ResourceExhaustedError. Probably my machine's GPU VRAM 6GB is not enough.

## I tried Google Colab, and got an annoying result

In [the previous post](https://mitsuoxv.rbind.io/2020/07/17/update-let-potus-speak/), my trial in Google Colab failed due to time out. In the retrospect, I may have forgotten to enable GPU by Edit > Notebook settings. This time I enabled GPU. It took about one and half hour to finetune the model. The result is [gpt_2_colab.ipynb](https://github.com/mitsuoxv/erp/blob/master/gpt_2_colab.ipynb).

I seeded the text, "I have some proposals to the Congress." The finetuned model continued:

"One way or the other, we will pursue the issues that matter most to us—jobs, growth, and economic opportunity—that will lead to sustained economic growth and to free trade and international economic cooperation."

After that, it copied the lines from #240 to #284 of the input texts, reagan.txt, I used for finetuning. Is it overfitting? I don't know.
