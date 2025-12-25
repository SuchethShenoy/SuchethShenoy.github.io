---
title: "Table Tennis Stroke Detection and Recognition Using Ball Trajectory Data"
collection: publications
category: manuscripts
permalink: /publication/2023-table-tennis-ball
excerpt: "Stroke recognition using ball trajectory data for table tennis analytics."
date: 2023-02-01
venue: "arXiv"
paperurl: "https://arxiv.org/pdf/2302.09657"
citation: "Kulkarni, K. M., Jamadagni, R. S., Paul, J. A., & Shenoy, S. (2023). <i>Table Tennis Stroke Detection and Recognition Using Ball Trajectory Data</i>. arXiv:2302.09657."
---

**Abstract**  
In this work, the novel task of detecting and classifying table tennis strokes solely using the ball trajectory has been explored. A single camera setup positioned in the umpire's view has been employed to procure a dataset consisting of six stroke classes executed by four professional table tennis players. Ball tracking using YOLOv4, a traditional object detection model, and TrackNetv2, a temporal heatmap based model, have been implemented on our dataset and their performances have been benchmarked. A mathematical approach developed to extract temporal boundaries of strokes using the ball trajectory data yielded a total of 2023 valid strokes in our dataset, while also detecting services and missed strokes successfully. The temporal convolutional network developed performed stroke recognition on completely unseen data with an accuracy of 87.155%. Several machine learning and deep learning based model architectures have been trained for stroke recognition using ball trajectory input and benchmarked based on their performances. While stroke recognition in the field of table tennis has been extensively explored based on human action recognition using video data focused on the player's actions, the use of ball trajectory data for the same is an unexplored characteristic of the sport. Hence, the motivation behind the work is to demonstrate that meaningful inferences such as stroke detection and recognition can be drawn using minimal input information.
