+++
title = "Price and spec of cloud based GPU"
date = 2018-10-29T14:17:43+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Handuo"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Info"]
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = true

+++

I summarized several cloud based GPU services:

| Name of services | Specification | Price (US$) |
| -----|------| :-------------:|
|AWS P2 instance | p2.xLarge  | 0.9 / hour |
|Azure NC6 | 1xK80 | 0.9 / hour|
|[Lambda GPU cloud](https://lambdalabs.com/service/gpu-cloud) | 8x AWS P2 instances | 0.90 / GPU/ hour |
|[NTU HPCC](https://ts.ntu.edu.sg/sites/hpc/Charges/Home.aspx) | 2 units of 1-P100 is scheduled to be ready by End of October | 0.78 / core/ hour |
