# Polygon Shape Detection – Squares, Rectangles & Triangles (OpenCV)

This document summarizes the **core concepts, formulas, and OpenCV functions** used to detect **triangles, rectangles, and squares** in an image using contour-based techniques.

---

## 1. Overall Approach (High-Level Pipeline)

Polygonal shape detection generally follows these steps:

```
Input Image
 ↓
Grayscale Conversion
 ↓
Thresholding / Edge Detection
 ↓
Contour Detection
 ↓
Polygonal Approximation
 ↓
Shape Analysis (vertices, aspect ratio, area)
 ↓
Draw & Label Shapes
```

---

## 2. Image Preprocessing

### Purpose

* Simplify the image
* Separate shapes from background

### Common Steps

* Convert to grayscale
* Apply thresholding to get a binary image

Binary images make contour detection reliable.

---

## 3. Contour Detection – `cv2.findContours()`

### Concept

Contours represent the **boundaries of objects** as a sequence of points.

### Function

```python
contours, hierarchy = cv2.findContours(image, mode, method)
```

### Important Parameters

* `image` → binary (single-channel)
* `mode`:

  * `cv2.RETR_EXTERNAL` → outer contours only
  * `cv2.RETR_TREE` → full contour hierarchy
* `method`:

  * `cv2.CHAIN_APPROX_SIMPLE` → compresses redundant points

Each contour is a NumPy array of `(x, y)` coordinates.

---

## 4. Perimeter & Area Calculations

### Perimeter – `cv2.arcLength()`

```python
perimeter = cv2.arcLength(contour, True)
```

Used to:

* Measure contour length
* Define approximation accuracy

---

### Area – `cv2.contourArea()`

```python
area = cv2.contourArea(contour)
```

Used to:

* Remove small noise contours
* Compare shape sizes

---

## 5. Polygonal Approximation – `cv2.approxPolyDP()`

### Concept

Simplifies a contour into a polygon with **fewer vertices**, making shape classification easier.

### Function

```python
approx = cv2.approxPolyDP(contour, epsilon, True)
```

### Epsilon Formula (Best Practice)

```
epsilon = 0.02 × perimeter
```

* Smaller epsilon → more vertices
* Larger epsilon → fewer vertices

The number of vertices defines the shape.

---

## 6. Shape Classification Logic

### Triangle Detection

* Number of vertices = **3**

```python
if len(approx) == 3:
    shape = "Triangle"
```

---

### Rectangle & Square Detection

Both have **4 vertices**, so further checks are needed.

---

## 7. Bounding Box & Aspect Ratio – `cv2.boundingRect()`

### Concept

Finds the smallest upright rectangle enclosing the contour.

### Function

```python
x, y, w, h = cv2.boundingRect(approx)
```

### Aspect Ratio Formula

```
Aspect Ratio = w / h
```

### Shape Decision

* **Square** → aspect ratio ≈ 1

  * Typical range: `0.95 – 1.05`
* **Rectangle** → aspect ratio significantly ≠ 1

---

## 8. Drawing Contours – `cv2.drawContours()`

### Purpose

Visualize detected shapes.

### Function

```python
cv2.drawContours(image, [approx], -1, (0, 255, 0), 2)
```

* Color is in **BGR**
* Thickness controls line width

---

## 9. Labeling Shapes – `cv2.putText()`

### Purpose

Annotate detected shapes.

### Function

```python
cv2.putText(image, shape, (x, y), cv2.FONT_HERSHEY_COMPLEX, 0.6, (255, 0, 0), 2)
```

Used to label:

* Triangle
* Square
* Rectangle

---

## 10. Key Interview Takeaways

* Contours = object boundaries
* Polygon approximation reduces noise
* Vertices count → shape type
* Aspect ratio distinguishes squares vs rectangles
* All detection is **geometry + thresholds**

---

## 11. One-Line Summary

> Polygon detection finds contours, approximates them into vertices, and classifies shapes using vertex count, aspect ratio, and area.

---

This structure is **interview-ready and implementation-ready**.

If you want next:

* **Complete working code example**
* **Visual diagram explaining each step**
* **Interview Q&A on contour-based shape detection**

# Circle Detection – Hough Circle Transform

## Hough Circle Transform – Core Idea

The Hough Circle Transform detects circular shapes by mapping edge points from image space into a **parameter space** defined by circle parameters **(x, y, r)**.

A circle equation:
(x − a)² + (y − b)² = r²

Each edge pixel votes for all possible circles passing through it. Strong peaks in the accumulator indicate detected circles.

OpenCV uses **Hough Gradient Method**, which:

* Uses image gradients to reduce search space
* Uses a 2D accumulator instead of 3D
* Is faster and more practical

---

## Preprocessing – `cv2.medianBlur()`

Median blur removes noise while preserving edges.

**Why median blur is used:**

* Removes salt-and-pepper noise
* Preserves sharp edges (important for circles)
* Improves edge detection reliability

Example:

```python
blurred = cv2.medianBlur(gray, 5)
```

---

## `cv2.HoughCircles()` Parameters

```python
circles = cv2.HoughCircles(
    image, cv2.HOUGH_GRADIENT, dp, minDist,
    param1=100, param2=30,
    minRadius=10, maxRadius=100
)
```

### Key Parameters Explained

* **dp**: Inverse ratio of accumulator resolution to image resolution
* **minDist**: Minimum distance between detected circle centers
* **param1**: Upper threshold for Canny edge detection
* **param2**: Accumulator threshold (higher = fewer circles)
* **minRadius / maxRadius**: Expected radius range

---

## Drawing Circles – `cv2.circle()`

```python
cv2.circle(img, (x, y), r, (0,255,0), 2)
```

---

# Polygon Detection – Square, Rectangle, Triangle

## General Pipeline

1. Convert to grayscale
2. Threshold / edge detection
3. Find contours
4. Approximate polygons
5. Classify shapes

---

## Contour Detection – `cv2.findContours()`

Contours represent object boundaries.

```python
contours, _ = cv2.findContours(binary, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
```

---

## Polygon Approximation – `cv2.approxPolyDP()`

Reduces contour points to polygon vertices.

Formula:
ε = α × arcLength

```python
epsilon = 0.04 * cv2.arcLength(cnt, True)
approx = cv2.approxPolyDP(cnt, epsilon, True)
```

---

## Area & Perimeter

```python
area = cv2.contourArea(cnt)
perimeter = cv2.arcLength(cnt, True)
```

---

## Rectangle & Square Detection

Use bounding box and aspect ratio:

```python
x, y, w, h = cv2.boundingRect(approx)
aspect_ratio = w / float(h)
```

* **Square** → vertices = 4 and aspect_ratio ≈ 1
* **Rectangle** → vertices = 4 and aspect_ratio ≠ 1

---

## Triangle Detection

* vertices = 3

---

## Drawing & Labeling

```python
cv2.drawContours(img, [approx], -1, (0,255,0), 2)
cv2.putText(img, "Rectangle", (x,y-10), cv2.FONT_HERSHEY_SIMPLEX, 0.6, (255,0,0), 2)
```

---

# Template Matching – Normalized Correlation

## Core Principle

Template matching slides a template over an image and computes similarity using **normalized cross-correlation**, making it robust to lighting changes.

### Formula

R(u,v) = Σ(T′·I′) / √(ΣT′² · ΣI′²)

Where mean is subtracted:
T′ = T − mean(T)
I′ = I − mean(I)

---

## Mean Subtraction – Why It Matters

* Illumination invariant
* Focuses on patterns, not brightness

---

## Correlation – `scipy.signal.correlate2d()`

```python
c = correlate2d(img, template, mode='same')
```

Produces a correlation map.

---

## Finding Best Match

```python
y, x = np.unravel_index(np.argmax(c), c.shape)
```

Translate to top-left corner:

```python
top_left = (x - w//2, y - h//2)
```

---

## Drawing Match – `cv2.rectangle()`

```python
cv2.rectangle(img, top_left, (top_left[0]+w, top_left[1]+h), (0,0,255), 2)
```

---

# Colour Detection – RGB / HSV Masking

## Core Idea

Detect colors by defining pixel intensity ranges.

---

## Mask Creation – `cv2.inRange()`

```python
mask = cv2.inRange(img, lowerb, upperb)
```

White → target color
Black → others

---

## Applying Mask – `cv2.bitwise_or()`

```python
result = cv2.bitwise_or(img, img, mask=mask)
```

---

## Importance of Thresholds

* Too wide → false positives
* Too narrow → missed detections

---

# Line Detection – Probabilistic Hough Transform

## Hough Line Principle

Lines are represented as:

ρ = x·cosθ + y·sinθ

Votes in (ρ, θ) space identify lines.

---

## Why HoughLinesP

* Faster
* Returns line segments directly
* Handles broken lines

---

## Preprocessing

### Gaussian Blur

```python
blur = cv2.GaussianBlur(img, (5,5), 0)
```

### Canny Edge Detection

```python
edges = cv2.Canny(blur, 50, 150)
```

---

## `cv2.HoughLinesP()` Parameters

```python
lines = cv2.HoughLinesP(
    edges, rho=1, theta=np.pi/180, threshold=15,
    minLineLength=50, maxLineGap=10
)
```

* **rho**: Distance resolution
* **theta**: Angle resolution
* **threshold**: Minimum votes
* **minLineLength**: Short line rejection
* **maxLineGap**: Join broken segments

---

## Drawing Lines – `cv2.line()`

```python
cv2.line(img, (x1,y1), (x2,y2), (255,0,0), 3)
```

---

## Interview Tip

> Hough Transform converts geometry detection into a voting problem in parameter space, making it robust to noise and partial occlusion.
