+++
title = "You only look once (YOLO) -- (2)"
date = 2018-08-20T16:21:12+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Handuo"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["ML", "Notes"]
categories = ["Object Detection"]

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = "yolo/intro_yolo_cars.jpeg"
caption = ""
image_preview = "yolo/intro_yolo_cars.jpeg"
preview = true

image:
    caption = "Vehicle Detection Result"
    focal_point = ""
    preview_only = false

+++
YOLO has higher localization errors and the recall (measure how good to locate all objects) is lower, compared to SSD. YOLOv2 is the second version of the YOLO with the objective of improving the accuracy significantly while making it faster.

The backbone network architecture of YOLO v2 is as follows:
![Yolo2 Backbone](/img/yolo/yolo2_net.jpg)

## 1. Accuracy Improvements

### Batch Normalization

Also removes the need of dropouts. mAP increases by 2%.

### High-resolution Classifier

To generate predictions with shape of $7\times 7 \times 125$, we replace the final fully connected layers with a  $3\times 3$ `convolution layer` each outputting 1024 output channels. Then we apply a final $1\times 1$ convolutional layer to convert the $7\times 7 \times 1024$ output into $7\times 7 \times 125$ and retrain it end-to-end. This makes training easier and moves mAP up by 4%.

### Convolution with Anchor Boxes

Early training is susceptible to unstable gradients. Arbitrary guesses on the boundary boxes may result in steep gradient changes.

In real life, boudnary boxes are not arbitrary. So the author create 5 **anchor** boxes with the following shapes.

![5 anchor boxes](/img/yolo/anchor_box.jpeg)

Instead of directly predicting 5 arbitrary boundary boxes, we predict offsdets to each of the anchor boxes. If we **constrain** the offset values, we can maintain the diversity of the predictions and have each prediction focusing on specific shape. So the initial training will be more stable.

### Dimension Clusters

In many problem domains, the boundary boxes have strong patterns. For example, in the autonomous driving, the 2 most common boundary boxes will be cars and pedestrians at different distances. To identify the top-K boundary boxes that have the best coverage for the training data, we run K-means clustering on the training data to locate the centroids of the top-K clusters.

Since we are dealing with boundary boxes rather than points, we cannot use the regular spatial distance to measure datapoint distances. No surprise, we use IoU.

### Direct location prediction

We make predictions on the offsets to the anchors. Nevertheless, if it is unconstrained, our guesses will be randomized again. YOLO predicts 5 parameters (tx, ty, tw, th, and to) and applies the sigma function to constraint its possible offset range.

![Location prediction on anchors](/img/yolo/yolo2_location_predict.jpeg)

With the use of k-means clustering (dimension clusters) and the improvement mentioned in this section, mAP increases 5%.

