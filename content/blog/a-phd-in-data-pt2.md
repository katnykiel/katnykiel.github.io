---
title: A PhD, in Data (Part 2)
toc: true
draft: true
breadcrumbs: false
date: 2026-03-04
---

Last December, I stumbled across the finish line and successfully defended my thesis in front of my committee. The six months prior to that, I had been facing burnout and dreaded working on my thesis. It's been five months since then, and the distance has helped me gain some perspective on the work that I did. I've come to really enjoy this field again, and here, I hope to share a bit more of what makes me love computational materials science.

Computational materials science, which uses predictive modeling to discover, design, and characterize materials, sits at the intersection of materials science, quantum mechanics, computer science, and machine learning. This meant that I had to take many disparate graduate courses and maintain expertise in many domains; exhausting, but fun. Among the many methods of computational materials science, I near-exclusively used **density functional theory** (DFT). This method, which won the [1998 Nobel Prize](https://www.nobelprize.org/prizes/chemistry/1998/8811-the-nobel-prize-in-chemistry-1998/), really deserves a ten-part series describing its theory, importance, and limitations. But in short: DFT approximates the many-body Schrödinger equation with a set of one-electron equations, each adding in an exchange-correlation (read: pseudo-magic) contribution from a functional of the electron density. While this formalism is equivalent, some approximations get taken along the way (i.e. which pseudo-magic term do you use?). In the end, DFT ends up being pretty good most of the time; which results in it being widely used in this field. DFT simulations can be cheap for systems with just a few low-atomic number atoms, running on a laptop in a few minutes, but they get expensive with bigger and more complex systems, taking weeks to run on large supercomputers. In the last few years, there's increasingly been a push to train machine learning models on DFT, to get near-DFT accuracy at a fraction of the cost. However, most of the work during my PhD was running DFT run on supercomputers, and I spent a lot of time implementing infrastructure to orchestrate and track these DFT workflows. Here, I want to ask the following questions:

{{< callout >}}
How much DFT did I run during my PhD? On what? How much energy did it take, and how would it compare to synthesizing these materials?
{{< /callout >}}

## How much DFT did I run during my PhD? On what?

- what DFT did I run throughout my PhD?
  - elements - what systems did I study?
  - simulations
![heatmap of frequency of each element](element-heatmap.png)
![pie chart of task type in db](db-tasks.png)

## How much energy did it take?

- How expensive is DFT?
  - CPU hours

## How would it compare to synthesizing these materials?

  - furnace power

## Simulation Data


