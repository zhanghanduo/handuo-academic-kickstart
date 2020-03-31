+++
title = "Multiple Object Tracking With Attention to Appearance, Structure, Motion and Size"
date = 2019-08-07T17:12:30+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Karunasekera Hasith", "Han Wang", "Handuo Zhang"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["2"]

# Publication name and optional abbreviated version.
publication = "IEEE Access Xplore"
publication_short = "IEEE Access"

# Abstract and optional shortened version.
abstract = "Objective of multiple object tracking (MOT) is to assign a unique track identity for all the objects of interest in a video, across the whole sequence. Tracking-by-detection is the most common approach used in addressing MOT problem. In this work, we propose a method to address MOT by defining a dissimilarity measure based on object motion, appearance, structure, and size. We calculate the appearance and structure-based dissimilarity measure by matching histograms following a grid architecture. Motion and size for each track are predicted using the information from track’s history. These dissimilarity values are then used in the Hungarian algorithm, in the data association step for track identity assignment. In addition, we introduce a method to address any false detection  stable tracks. The proposed method runs in real time following an online approach. We evaluate our method in both MOT17 benchmark data-set for pedestrian tracking and KITTI benchmark data-set for vehicle tracking using the same system parameters to verify the robustness of the proposed method. The method can achieve state-of-the-art results in both benchmarks."
abstract_short = ""

# Featured image thumbnail (optional)
image_preview = "tracking_flow.png"

# Is this a selected publication? (true/false)
selected = true

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's filename without extension.
#   E.g. `projects = ["deep-learning"]` references `content/project/deep-learning.md`.
#   Otherwise, set `projects = []`.
projects = []

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Tracking"]

# Links (optional).
url_pdf = ""
url_preprint = ""
url_code = ""
url_dataset = ""
url_project = ""
url_slides = ""
url_video = ""
url_poster = ""
url_source = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]

# Does this page contain LaTeX math? (true/false)
math = false

# Does this page require source code highlighting? (true/false)
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
image_preview = "tracking_flow.png"
caption = "Flow chart of the proposed tracking framework"
preview = true
+++
