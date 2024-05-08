# OBJECT DETECTION: Evaluation Metrics <a id="object-detection-evaluation-metrics"></a>

### 1. **Intersection over Union (IoU) ( Jaccard’s Index ) :**

 calculated by taking the intersection area of the predicted bounding box and the ground truth bounding box and dividing by the union of the same. It provides a numerical value that indicates how well the model’s prediction aligns with the actual object location.![](https://lh7-us.googleusercontent.com/gpnfoo3kRjTQ460sMGohlRM666If6MmEVBdrC96ajc-e_pv4MFAhn7AfulNen2L1hLW965dpnzrAU7kkI82bF6ED_wZxPwxITjm9Xmnu4GTM3rlo9tdoRr9TyVO5ITkj2SdNEGJJpYOYrzJ5_NNWz1k)

### 2. **Precision-recall curve/Average Precision (AP):**

First, we need to understand what is recall and precision and their significance in the context of object detection.

Precision focuses on accurately identifying relevant objects, while recall checks the model’s ability to find all ground truth or say to capture all relevant objects/classes in the image.

![](https://lh7-us.googleusercontent.com/Knjh_DBvWq9ilwiwOYmjGxfgNI2s59zNlU9Jtd5p9j_XWbNYijS-RJPCCdwbBJl7Jsn-EdaDwYGGieewgdsRcphvVU4Th-bgivgY4w27Ly6Qrxy7gNy_wCGHBY_Q1H__1StTGkdKxogRIGi8Ee-_4TE)

To understand True positive (TP), False positive (FP), False Negative (FN), True Negative (TN), please refer to this example:

Detecting the presence of trees in an image, the positive class may be "Tree", while the negative class would be "No Tree". A true prediction occurs when the prediction is correct, and a false prediction occurs when the prediction is incorrect.

![](https://lh7-us.googleusercontent.com/ohW9Xwc88obve25XhELT0NFUz0WvoYEtFrOE8VdQeo2ULJDiPLkcHAv5AI3jr5epxrmcj0VE01pUdHM5bnaUTl5xMKP8Bd8TWPZ1i02olgJZcqCYXVQZgX6Kmb19UNYDhYIitbIMi-mKmGGdY_CYhb8)

[for more detail](https://pro.arcgis.com/en/pro-app/latest/tool-reference/image-analyst/how-compute-accuracy-for-object-detection-works.htm)

Now back to the **precision-recall curve**, (formed by computing precision-recall values at different confidence thresholds) it serves as an evaluation of the performance of an object detection model. The model is considered a good predictive model if the **precision stays high as the recall increases**.

OR we can say, that AUC (Area under Curve), which represents AP, is higher indicating superior model performance.

### 3. **Mean Average Precision (mAP):**  computes the average AP across multiple confidence thresholds.

![](https://lh7-us.googleusercontent.com/EHsmEsd3JIG184pwJxqXIc82vZ_zM72Hf8OaNlWEyj7z8w004UiPYdCWrIbA0XmWklimuX4ZLsfbyavIRtwf2V-71pjOqVTLRVd-MZHDt3N91kmlTEsirnUICs50mmlC5cdcvWfKR0P6VcMDIpfC2UA) <https://kili-technology.com/data-labeling/machine-learning/mean-average-precision-map-a-complete-guide>

### 4. **F1 - Score:** 

Is the harmonic mean of precision and recall. It provides a balanced measure of the model’s performance, considering both false positives and false negatives. This metric is particularly useful when there is an imbalance between positive and negative classes in the dataset.


# Open Source Evalv Metrics Toolkit:  [Github\_link](https://github.com/rafaelpadilla/review_object_detection_metrics/blob/main/docs/formats.md)<a id="open-source-evalv-metrics-toolkit-github_link"></a>

### 1. Input requirement to use this tool kit: 

- Bounding box format:  It supports more than 8 different kinds of annotation formats.

![](https://lh7-us.googleusercontent.com/iwryxk9TU01b52jIuucaqwrsUfjweunUejGU6fdcKWifiZ8BqLc-Q-7iPelDMli6mBiG1qt9jeBsJ8pfjFdmAb0wWOyFWtfU_zZR2K2ZZhPrACb7M51fB0Iwshw7HO5_QSycWfODaCJ036ZDvOZM04o)

1. Labelme Ground truth BB format: .xml
```
<bndbox>
   <xmin>x</xmin> <ymin>y</ymin> <xmax>x+w</xmax> <ymax>y+h</ymax>
 </bndbox>
```

3. COCO BB format: in JSON 

```[x_min, y_min, width, height]```

3. PASCAL VOC BB Format: .xml

```[x_min, y_min, x_max, y_max]```

4. YOLO BB Format: .txt/text format

```[x_center, y_center, width, height]```

Similarly, we can look into all BB formats, this tool supports almost all formats.


### How to use this tool <a id="how-to-use-this-tool"></a>

-Clone repo first in the working directory

  1. Create Conda environment using `environment.yml` in repo
  
  2. conda env create -n `<env_name>` --file environment.yml
  
  3. conda activate `<env_name>`
  
  4. python setup.py install ## Install Tool
  
  5. python `run.py`        ## RUN the GUI

### GUI will look like this: 

![](https://lh7-us.googleusercontent.com/vXM7K4kgqQiRZfqrN4gYMcaCfEoS4J2EtfSoZ8tryjFVx9V77-5LNimveOczyFcNrjPUUESjEWxUDw-QidD295mgOlEAqgH4YJZ8teeA2GVY7E00nTF2iAYP9SPGeQzhQ26xCSYxjvvSx1fFISsRqqE)

**8. Coordinate formate**: formate of file to represent detections

**5. Ground-truth statistics(Optional)**: provides the amount of bounding boxes of each ground-truth class and visualizes the images with bounding boxes

**7. Classes**: .txt file with class name with IDs (single class in each line).  Use If your coordinates formats represent the classes with IDs 

**11. Output**: Choose/Create a folder where PASCAL VOC AP plots will be saved.

**12. Result**: Window pops up, containing values of all metrics. 


### A brief about the Evalv metrics toolkit has considered<a id="a-brief-about-the-evalv-metrics-toolkit-has-considered"></a>

-**AP@t** : Average Precision at IOU = t


-**AP@[.5:.05:.95]**: Starting with IOU threshold from 50% to 95% with step difference of 5%.<a id="ap50595--starting-with-iou-threshold-from-50-to-95-with-step-difference-of-5"></a>

-**APS, APM, and APL**: APS only evaluates the ground-truth objects of small sizes (area < 32^2 pixels); APM considers only ground-truth objects of medium sizes (32^2 < area < 96^2 pixels); APL considers large ground-truth objects (area > 96^2) only.<a id="aps-apm-and-apl-aps-only-evaluates-the-ground-truth-objects-of-small-sizes-area--322-pixels-apm-considers-only-ground-truth-objects-of-medium-sizes-322--area--962-pixels-apl-considers-large-ground-truth-objects-area--962-only"></a>

![](https://lh7-us.googleusercontent.com/bs0MEnimHl_lMOfXiXtw9UPjMEVcSwjoOF7xsdK70cuCXcod1a8ML7NCy3kkOWs2DMGDUzn41XxhRweZezEKGPTXIYsSSzfwhp9zn3ZV3fCPpuJ_AvmFbw6QxpATcbHNXXTr9ousD8tLIXZe9FmZVz0)

![](https://lh7-us.googleusercontent.com/vbBgFqWHFu1Cqd08mHTFAgVLH-beICVlUaLSVwwuPPC6eHdTgRw468xDH2Y-1Uii9KGw1mnPdX-ybzdTf_5mciq5gradNWNcQovZLT96wGCANs-VFrnjMEcI5vW8qgHF-IFWvSXVZTXwIyXx5Te7naA)

Here we will be using Yolo v8 format: \[x\_center, y\_center, width, height] 


### GUI View: On local System<a id="gui-view-on-local-system"></a>

Examples being used here, is already present in[ GitHub repo](https://github.com/rafaelpadilla/review_object_detection_metrics/tree/main/data/database), in all formats supported by this toolkit.

![](https://lh7-us.googleusercontent.com/iQNHDQcuVCRATzRs68nuJAu5fWgb3TLAYR4_fK2kqBe0JPVyYkmrMcKxVChQXUfvZ8CSf1cIEM6K1U1QMiqG5GnkCa_ll0mpTa96ughNT2ozkwn6XDNCJAMOmK3aLX2KFqaZGqKLqQ2G6XNshZfc890)

-**RESULT**: 

![](https://lh7-us.googleusercontent.com/LUg5xgL7Obj_gyTMdgjhKVgiPHC2CuasLJnhvkVahm47NtBclGyKEu3Y1AE2JY9ck4cTGqw4rSNfu2cVvuermIvMW5QC3FgFwMfq9xCyBF8gtwXExovwA3dn_Xx31CsnesVlzT73ocm6YfkuMmN1_kQ)

-**Output Folder**: 

![](https://lh7-us.googleusercontent.com/QkEPrm34GdU7BCja8i_gMXAHs1945LeAFkbOGNnR1Wl3nPqDJPj61F3sAQQ3jM5MZHzJk3OKeXigrepqBjvxU8Kfg2R1ttFOq6E6z4Uz6_L2I-SNaJE7RXh-hZli6Y5H56vJlSlz1PpUXadVuV513HY)

### References: 

<https://pro.arcgis.com/en/pro-app/latest/tool-reference/image-analyst/how-compute-accuracy-for-object-detection-works.htm>

<https://labelyourdata.com/articles/object-detection-metrics>

<https://medium.com/@henriquevedoveli/metrics-matter-a-deep-dive-into-object-detection-evaluation-ef01385ec62>
