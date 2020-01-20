---
title: Deep Learning For Solving PDE's
summary: My graduate research project
tags:
- Finite Element Method, Deep Learning
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

image:
  caption: 
  focal_point: Smart



# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

Partial differential equations (PDEs) are equations that contains unknown multivariable functions and their partial derivatives. PDEs can be used to describe a wide variety of phenomena such as heat, diffusion,fluid dynamics, quantum mechanics, etc. 
 
Traditional methods for solving PDEs include Finite Element Methods (FEM), Finite Difference Methods (FDM) and Finite Volume Methods (FVM). In recent years, researchers start to develop deep neural networks (DNNs), also known as deep learning, for solving PDEs.
 
Using DNNs achieves better flexibility than traditional computational methods. A DNN model only needs to be trained once to repeatedly generate precise solutions for a whole family of PDEs. Besides, it often consumes less computational power. 
 
My graduate research focuses on developing DNNs for solving the Navier-Stokes equations, which describe the dynamics of viscous fluid.