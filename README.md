# 💧 Waterpixels: Superpixel Segmentation using Watershed Transform

This project implements and analyzes the performance of a superpixel segmentation method called **Waterpixels**, which produces contour-adherent segments using a watershed-based algorithm.

## 📘 Project Overview

Based on the method described in the article *"Waterpixels"*, the goal is to implement two variants of waterpixels:

- **c-waterpixels**: superpixels based on regular grid cell centers
- **m-waterpixels**: superpixels using extinction regions of minimal gradient

## 🧩 Methodology

### Step-by-step Process:
1. Compute the **morphological gradient** of the grayscale or HSV image.
2. Generate a **grid of cells** (square or hexagonal) over the image.
3. Choose **markers** for each cell:
   - Center (for c-waterpixels)
   - Extinction region barycenter (for m-waterpixels)
4. Compute a **regularized gradient** using: greg = g + k * dQ
where `dQ` is the distance to the nearest marker.
5. Apply the **watershed algorithm** using OpenCV.

---

## 🔬 Variants

### ◼️ c-Waterpixels
- Use square or hexagonal cells with fixed markers at the center.
- Simpler and faster to implement.
- Slightly better alignment with image contours in tests (~87.19% vs 85.83%).

### 🔷 m-Waterpixels
- Markers are chosen as the barycenter of the largest extinction zone in the cell.
- Potentially better contour adherence in some cases.
- Slightly slower due to extra gradient analysis.

---

## 🧪 Parameter Sensitivity

- **`k` (gradient regularization):**
- Low `k` → better contour adherence, irregular shapes
- High `k` → smoother, regular shapes, but may miss fine details

- **Cell spacing:**
- Too small → too many superpixels
- Too large → loss of important details
- Optimal spacing ≈ 1/10 of image width (empirically)

---

## 🎨 Color Support

- Input RGB images are converted to **HSV**
- Gradients computed per channel then averaged
- This allows better segmentation for color images, closer to human perception

---

## ⏱️ Performance

- **Linear time complexity** in the number of pixels
- `c-waterpixels` are faster than `m-waterpixels`
- Hexagonal grids take slightly longer than square grids due to norm calculations

---

## ⚙️ Technologies Used

- **Python**
- **NumPy** / **Matplotlib**
- **OpenCV**:
- `cv2.morphologyEx`, `cv2.watershed`, `cv2.connectedComponentsWithStats`
- `cv2.cvtColor`, `cv2.split`, `cv2.normalize`, `cv2.findContours`

---

## 📸 Example Results

- Visualizations compare various configurations (k, spacing, cell types)
- Overlap between contours from waterpixels and real image contours is computed using OpenCV

---

## 👥 Authors

- **Noé Mosca**
- **Baptiste Vibert**

Project completed as part of a computer vision module (IMA05 final project).
