# Image Distributions – Histogram, PDF & CDF (Layman Explanation)

This document explains the **concepts and formulas** in very simple terms. It includes **examples** and **commonly asked interview questions with answers**.

---

## 1. What Does “Image Distribution” Mean?

### Concept (Layman Terms)

An image distribution tells us:

> **How pixel values are spread across an image**

In simple words:

* How many pixels are dark?
* How many pixels are bright?
* Is the image mostly dark, bright, or balanced?

This information helps us **analyze, enhance, and compare images**.

---

## 2. Pixel Intensity Values

### Concept

* Grayscale image pixel values range from **0 to 255**

  * `0` → Black
  * `255` → White

Each pixel contributes **one value** to the distribution.

### Example

If an image has mostly values between 0–50 → image is **dark**.

---

## 3. Histogram

### Concept (Very Simple)

A **histogram** is a bar chart that shows:

> How many pixels have a particular intensity value

### X-axis

* Pixel intensity (0–255)

### Y-axis

* Number of pixels

### Formula (Intuition)

```
Histogram(i) = Number of pixels with intensity i
```

### Example

* Many bars on the left → dark image
* Many bars on the right → bright image

### Why Histogram is Important

* Understand lighting conditions
* Detect underexposed or overexposed images
* Used in contrast enhancement

---

## 4. Normalized Histogram

### Concept

A normalized histogram shows **percentage of pixels**, not absolute counts.

### Formula

```
Normalized Histogram(i) = Histogram(i) / Total number of pixels
```

### Why Normalize?

* Makes comparison easier between images of different sizes
* Values lie between **0 and 1**

### Example

If value = 0.2 → 20% of pixels have that intensity

---

## 5. Probability Density Function (PDF)

### Concept (Layman Terms)

PDF tells us:

> Probability of finding a pixel with a certain intensity

In images:

```
PDF ≈ Normalized Histogram
```

### Formula

```
PDF(i) = Number of pixels with intensity i / Total pixels
```

### Example

If PDF(100) = 0.05 → 5% of pixels have intensity 100

### Why PDF is Useful

* Mathematical view of pixel distribution
* Foundation for image enhancement techniques

---

## 6. Cumulative Distribution Function (CDF)

### Concept (Very Simple)

CDF tells us:

> How many pixels have intensity **less than or equal to** a value

It is the **running sum of PDF**.

### Formula

```
CDF(i) = Σ PDF(j)  where j = 0 to i
```

### Properties

* Starts at 0
* Ends at 1
* Always increasing

### Example

If CDF(120) = 0.7 → 70% of pixels have intensity ≤ 120

---

## 7. Relationship Between Histogram, PDF & CDF

| Concept   | Meaning                          |
| --------- | -------------------------------- |
| Histogram | Raw count of pixels              |
| PDF       | Probability version of histogram |
| CDF       | Accumulated probability          |

Think of it as:

```
Histogram → PDF → CDF
```

---

## 8. Why Image Distributions Matter

Image distributions help in:

* Contrast stretching
* Histogram equalization
* Image comparison
* Computer vision preprocessing

### Real-Life Example

Medical imaging:

* Histogram shows poor contrast
* CDF helps redistribute pixel values
* Result → clearer scan

---

## 9. Practical Example (Simple)

Suppose an image has 10 pixels:

```
[0, 0, 50, 50, 50, 100, 100, 150, 200, 255]
```

Histogram:

* 0 → 2 pixels
* 50 → 3 pixels
* 100 → 2 pixels

PDF for 50:

```
3 / 10 = 0.3
```

CDF for 100:

```
(2+3+2) / 10 = 0.7
```

---

# Interview Questions & Answers

## Q1. What is an image histogram?

**Answer:**
An image histogram shows the distribution of pixel intensity values and tells us how bright or dark an image is.

---

## Q2. Difference between histogram and PDF?

**Answer:**
Histogram shows pixel counts, while PDF shows probability of pixel intensities.

---

## Q3. Why do we normalize a histogram?

**Answer:**
To convert pixel counts into probabilities and compare images of different sizes.

---

## Q4. What is CDF and why is it used?

**Answer:**
CDF is the cumulative sum of PDF and is used in contrast enhancement techniques like histogram equalization.

---

## Q5. What does a left-skewed histogram indicate?

**Answer:**
The image is mostly dark (underexposed).

---

## Q6. What does a right-skewed histogram indicate?

**Answer:**
The image is mostly bright (overexposed).

---

## Q7. How are histogram and CDF related?

**Answer:**
CDF is obtained by accumulating histogram values (after normalization).

---

## Q8. Where are image distributions used in real life?

**Answer:**

* Medical imaging
* Satellite images
* Face recognition preprocessing
* Quality inspection systems

---

## Q9. Can histogram work on color images?

**Answer:**
Yes, but histograms are computed separately for each color channel (R, G, B).

---

## Q10. Why are image distributions important in computer vision?

**Answer:**
They help understand image quality, improve contrast, and prepare images for further processing.

---

## Final Takeaway

If you understand:

* Histogram → what exists
* PDF → how likely
* CDF → how accumulated

You have mastered **image distribution fundamentals**, a key building block in computer vision interviews.
