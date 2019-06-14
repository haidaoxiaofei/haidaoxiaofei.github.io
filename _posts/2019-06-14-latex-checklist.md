---
layout: post
category: "research"
title:  "Checklist of Latex papers before submitting"
tags: [Latex]
---

### 1. Grammar Checking

- Recommend [textidote](https://github.com/sylvainhalle/textidote), which is a very useful latex-native grammar checking tool. It can go through latex source files and generate an elegant HTML report. However, it is still under development and some bugs may exist. You can also use [the branch](https://github.com/haidaoxiaofei/textidote) maintained by me with some bug fixes, however it needs you to compile by yourselves.
- Ask your colleagues to help you do proofreading

### 2. Check Overlaps

- Top and bottom of the figures, tables. Pay more attention on captions.
- Equations

### 3. Use the search function (Ctrl-f) of PDF to search:

- '?': any missing references or citations?

### 4. Blank space issues

- leave one blank space before '(' and after ')'
- for citation, use blabla~\cite{xxx}, which can avoid awkward line break putting citations (e.g., [2]) to the beginning of a new line.

### 5. Suggest to use eps format for figures

- Use online tools, such as [online-convert](https://www.online-convert.com/) to convert your figures (e.g., png, jpg) to eps format. Then, add \usepackage{epstopdf}.