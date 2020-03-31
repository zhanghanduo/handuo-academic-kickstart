+++
title = "Heading Reference-Assisted Pose Estimation for Ground Vehicles"
date = 2018-04-30T13:48:11+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Han Wang", "Rui Jiang", "Handuo Zhang", "Shuzhi Sam Ge"]

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
publication = "IEEE Transactions on Automation Science and Engineering"
publication_short = ""

# Abstract and optional shortened version.
abstract = "In this paper, heading reference-assisted pose estimation (HRPE) has been proposed to compensate inherent drift of visual odometry (VO) on ground vehicles, where an estimation error is prone to grow while the vehicle is making turns or in environments with poor features. By introducing a particular orientation as ``heading reference,'' a pose estimation framework has been presented to incorporate measurements from heading reference sensors into VO. A graph formulation is then proposed to represent the pose estimation problem under the commonly used graph optimization model. Simulations and experiments on KITTI data set and our self-collected sequences have been conducted to verify the accuracy and robustness of the proposed scheme. KITTI sequences and manually generated heading measurement with Gaussian noises are used in simulation, where rotational drift error is observed to be bounded. Compared with a pure VO, the proposed approach greatly reduces average translational localization error from 153.85 to 24.29 m and 23.80 m in self-collected stereo visual sequences with traveling distance over 4.5 km at the processing rates of 19.7 and 11.1 Hz, for the loosely coupled and tightly coupled models, respectively."
abstract_short = ""

# Featured image thumbnail (optional)
image_preview = "ahrs_tight.png"

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
tags = []

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
image = "ahrs_tight.png"
caption = ""

+++
