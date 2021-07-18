---
layout: post
title: "Notes on Dynamic Programming"
date: 2021-06-11 20:00:00 +0900
categories: Notes on Programming
---

## Introduction

As one prepares for job interviews, one would find themselves studying simple programming. 

If you are done with all the simple algorithm, I'll bet most of the people are stuck with so called **dynamic programming**.(If not you wouldn't have stumbled across this blog post anyway)

## Dynamic Programming

The essence of dynamic programming is that the whole technique is nothing more than **Recurrence Relation** that you learn in elementry math. 

In other words, if the question is related with dynamic programming, the question is basically asking you to figure out the relation between states. 

Take this for an example:

$$f(i) = f(i-1) + f(i-2)$$
$$where i \geq 2$$
<img src="https://render.githubusercontent.com/render/math?math=f(i) = f(i-1) + f(i-2)">

<img src="https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1">
