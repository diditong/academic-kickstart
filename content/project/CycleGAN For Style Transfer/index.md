---
title: Image to image translation using cycle GANs
summary: CS 547 Final Project
tags:
- GAN, Deep Learning
date: "2019-11-15T00:22:21Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: 
  focal_point: Smart

#links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
#url_code: ""
#url_pdf: ""
#url_slides: ""
#url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

**Project Purpose** <br/>
This is the final project for CS 547: Deep Learning offered by 
University of Illinois Urbana-Champaign in Fall 2019. The goal is to implement 
a Cycle-consistent Generative Adversarial Network (CycleGAN) model from scratch 
for image-to-image translation problems based on the paper [1].

**Project Deliverables** <br/>
Code for the following functions are written:
1. The discriminator & generator functions for CycleGAN
2. An object-oriented network structure of CycleGAN
3. The loss function
4. The training function

**Results** <br/>
The cover picture is the composition of a photo of my hometown in the style of Vincent 
van Gogh's paintings. Similar results are obtained from trainings on other datasets.


[1] Zhu, Jun-Yan, Taesung Park, Phillip Isola, and Alexei A. Efros. "Unpaired image-to-image
translation using cycle-consistent adversarial networks." In Proceedings of the IEEE international
conference on computer vision, pp. 2223-2232. 2017.
