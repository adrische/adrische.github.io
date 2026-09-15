---
layout: post
title:  "LLM access from within Jupyter notebooks"
date:   2026-06-19 12:07:03 +0200
---

I have recently come across [AnswerAI](https://answer.ai/), in particular their platform [SolveIt](https://solve.it.com/). It is a notebook-like interface that in addition to code and markdown cells has one additional type of cell, a prompt cell. Each prompt includes the current notebook up to that point as context. That allows you to get contextual help without leaving the notebook interface. They have also implemented all kinds of ways to get context into the notebook, from images, to screen sharing, to git repos.

I have implemented something similar (but much simpler) for Jupyter notebooks. Jupyter has something called [magic commands](https://ipython.readthedocs.io/en/stable/interactive/magics.html), these are commands that are prefixed by `%` (for line commands) or `%%` for cell commands and allow you to call a variety of functions. For example, you can call bash code with `%%bash`.

Besides the existing magic commands, IPython offers the possibility to define your own. So I made an `%ai` magic command that allows you to prompt an LLM from within a code cell. The prompt gets the current notebook up to that point as context which makes the result much more helpful than a plain prompt. You also don't need to leave your notebook environment.

The package is called 'aimagics', and is available with `pip install aimagics` from [Pypi](https://pypistats.org/packages/aimagics). The repo is on [Github](https://github.com/adrische/aimagics). The repo also contains for info on how to set it up and use it. It is my first publically available Python package! If you like it, or are interested in additional features, please let me know.

The package is basically a wrapper around existing AnswerAI repos, that they generously make publicy available. I give the same disclaimer as in the repo: 

> This repository would not be possible without the FastAI / AnswerAI open source packages, in particular [FastLLM](https://github.com/AnswerDotAI/fastllm). 

> There are a number of packages implementing basically the same ideas (just much better):

> - [AnswerDotAI/ai-jup](https://github.com/AnswerDotAI/ai-jup) An extension for Jupyter Lab
> - [AnswerDotAI/ipyai](https://github.com/AnswerDotAI/ipyai) An extension of IPython in the terminal
> - <https://nathancooper.io/blog/2026-08-10-ipython-is-all-you-need> An excellent blog post implementing these ideas much better for ipython.

> During the finishing stages I also found <https://pypi.org/project/aimagic/> on PyPi, which is also a package by AnswerAI and basically what I am implementing here, even with the same syntax and the same name, just for Jupyter (relying on Javascript to get the cells for context).

To offer some slight defense as to why my package might be useful in addition to those other existing ones: I rely on the saved state of the notebook on disc, and do not use Javascript to query the content of the existing cells. As soon as you use Javascript, your implementation becomes front end dependent (i.e., whether you use jupyer notebook, or vscode to access the notebook). The main advantage of my solution is therefore being independent of the front end.

Some other interesting resources that I have come across while developing this:
- A [talk by Bret Victor](https://www.youtube.com/watch?v=PUv66718DII) on having immediate feedback while programming (or doing anything, really)
- A [talk by Jeremy Howard](https://www.youtube.com/watch?v=SUZwYV5JYBM) on working jointly with AI, driven by your own intent
- The recordings of the SolveIt course. The sign up to SolveIt at time of writing is semi-open. If you find the singup page, you can find the course recording on the starting page, which I recommend
- The welcoming and open SolveIt community on [Discord](https://discord.gg/9nkG33kKbM)
- Iterative Python package development from within notebooks with [Nbdev](https://nbdev.fast.ai/)