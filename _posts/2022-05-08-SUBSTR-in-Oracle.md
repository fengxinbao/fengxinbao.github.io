---
layout: post
read_time: true
show_date: true
title:  SUBSTR in Oracle
date:   2021-05-08 13:32:20 -0600
description: Single neuron perceptron that classifies elements learning quite quickly.
img: posts/20210125/Perceptron.jpg 
tags: [Oracle]
author: Armando Maynez
github:  amaynez/Perceptron/
mathjax: yes
---

## Syntax

```sql
SUBSTR(char, position [,length])
```

Return a portion of `char`, beginning at charactor `position`，`length` characters long.

1.  If `position` is `0`，it is treated as `1`.
