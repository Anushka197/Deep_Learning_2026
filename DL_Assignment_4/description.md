# Object Detection Lab — From R-CNN to YOLO

## Introduction
In this lab, I explored how object detection methods have evolved over time. The main focus was to understand how older techniques worked, what their limitations were, and how newer models improved both speed and performance.

The work was done using a small dataset of fruit images (Apple, Banana, Orange), where the goal was to detect and classify objects in images. :contentReference[oaicite:0]{index=0}

---

## What I Learned

### 1. Understanding Object Detection Basics
I learned that object detection is not just about identifying what is in an image, but also *where* the object is located. This is done using bounding boxes.

A key concept I understood is **Intersection over Union (IoU)**:
- It measures how similar two bounding boxes are
- A higher IoU means better prediction
- It is important for evaluating model performance

---

### 2. Region Proposal Methods (R-CNN)
I studied how early object detection methods worked.

- **Selective Search** generates many possible regions in an image
- These regions are then passed one by one into a CNN

What I noticed:
- This approach is very slow
- The same image is processed multiple times
- There is a lot of repeated computation

This helped me understand why improvements were needed.

---

### 3. Improving Efficiency (Fast R-CNN)
Fast R-CNN improved the process by:
- Running the CNN only once on the full image
- Extracting features for each region from the same feature map

What I learned:
- Avoiding repeated work makes a big difference
- Sharing computation improves speed significantly

---

### 4. End-to-End Detection (Faster R-CNN)
Faster R-CNN introduced the **Region Proposal Network (RPN)**.

Instead of using Selective Search:
- The model itself generates region proposals
- Everything is trained together

Key understanding:
- Deep learning models can replace manual algorithms
- This makes the system faster and more accurate

---

### 5. Removing Duplicate Predictions (NMS)
I learned how **Non-Maximum Suppression (NMS)** works.

- It removes overlapping boxes
- Keeps only the most confident predictions

Important insight:
- Choosing the IoU threshold is important
- Too high → many duplicate boxes  
- Too low → may miss objects  

---

### 6. Real-Time Detection (YOLO)
Finally, I worked with YOLO (You Only Look Once).

- It predicts everything in one pass
- Much faster than previous methods
- Suitable for real-time applications

During training:
- I used a custom dataset
- Converted labels into YOLO format
- Trained YOLOv8 for multiple epochs

I also evaluated performance using:
- mAP@50
- mAP@50–95

---

## Key Takeaways

- Early models like R-CNN are accurate but inefficient  
- Fast R-CNN reduces repeated computation  
- Faster R-CNN makes the pipeline fully learnable  
- YOLO is the most efficient and practical for real-time use  

Overall, I understood how object detection improved step by step, and why modern approaches are designed the way they are.

---

## Challenges Faced

- Understanding how bounding boxes are calculated  
- Converting XML annotations into YOLO format  
- Managing large number of region proposals  
- Tuning thresholds in NMS  

These challenges helped me better understand the internal working of detection models.

---

## How to Run the Project

1. Open the notebook in Google Colab  
2. Install required libraries:
   ```bash
   pip install ultralytics torchvision
   pip install opencv-contrib-python
