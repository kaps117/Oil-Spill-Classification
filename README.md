```markdown
# OilSpillSense: SAR Image Analysis for Oil Spill Detection and Severity Estimation

---

### Project Overview

**OilSpillSense** is a computer vision and image processing pipeline leveraging **Synthetic-Aperture Radar (SAR)** imagery to automatically detect, segment, and assess the severity of oil spills in marine environments. Unlike traditional projects focused solely on spill identification, this work extends the analysis to **quantitative severity estimation**, providing actionable data for rapid environmental response.

---

### Key Features & Differences

- **Automated Severity Scoring:** Calculates spill area, perimeter, and spread rate—crucial for prioritizing response efforts.
- **Adaptive Image Processing:** Employs adaptive filtering and contrast enhancement tailored to each image’s unique noise and illumination characteristics.
- **Machine Learning Integration:** Uses statistical features from segmented spills to classify and score their severity, moving beyond simple binary detection.
- **Clear, Interpretable Outputs:** Delivers both visual segmentation masks and tabular metrics, supporting informed decision-making.

---

### Installation

1. **Clone the repository:**

```
git clone https://github.com/yourusername/OilSpillSense.git
cd OilSpillSense
```

2. **Create a virtual environment (recommended):**

```
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies:**

```
pip install -r requirements.txt
```

---

### Dataset

- **Source:** Sentinel-1 SAR images, focusing on regions with documented oil spills.
- **Format:** GeoTIFF or other compatible SAR image formats.
- **Folder Structure:** Place your SAR images in the `./data` directory.

---

### Usage

**Run the pipeline on a sample image:**

```
python main.py --image_path ./data/your_spill_image.tif
```

**Command-line arguments:**

| Argument         | Description                                    | Default            |
|------------------|------------------------------------------------|--------------------|
| `--image_path`   | Path to the SAR image to analyze               | Required           |
| `--output_dir`   | Directory for results and visualizations       | `./results`        |
| `--verbose`      | Print progress and debug information           | `False`            |

---

### Methodology

```
import cv2
import numpy as np
from skimage import exposure, filters, morphology
from sklearn.ensemble import RandomForestClassifier
import pandas as pd

# 1. Load and preprocess the SAR image
image = cv2.imread(args.image_path, cv2.IMREAD_GRAYSCALE)

# 2. Adaptive noise reduction
denoised = cv2.fastNlMeansDenoising(image, None, h=10, templateWindowSize=7, searchWindowSize=21)

# 3. Contrast enhancement (CLAHE)
clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8,8))
enhanced = clahe.apply(denoised)

# 4. Adaptive thresholding
thresh = cv2.adaptiveThreshold(enhanced, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 11, 2)

# 5. Morphological operations
kernel = np.ones((5,5), np.uint8)
opened = cv2.morphologyEx(thresh, cv2.MORPH_OPEN, kernel)

# 6. Edge detection
edges = cv2.Canny(opened, 100, 200)

# 7. Regionprops and feature extraction
from skimage.measure import label, regionprops
label_image = label(opened)
regions = regionprops(label_image)

# Extract features for each region
features = []
for region in regions:
    features.append([
        region.area,
        region.perimeter,
        region.mean_intensity,
        region.eccentricity,
    ])
features = np.array(features)

# 8. Severity estimation and classification (example: Random Forest)
# Load your pre-trained model or train one with labeled data
# clf = RandomForestClassifier(...)
# severity_scores = clf.predict_proba(features)

# 9. Save results
import matplotlib.pyplot as plt
plt.imshow(edges, cmap='gray')
plt.savefig(f"{args.output_dir}/edges.png")

results = pd.DataFrame(features, columns=['Area', 'Perimeter', 'Mean Intensity', 'Eccentricity'])
results.to_csv(f"{args.output_dir}/spill_metrics.csv", index=False)
```

---

### Output

- **Visualizations:** Edge-detected spill masks and enhanced images in `./results`.
- **Metrics Table:** CSV file (`spill_metrics.csv`) with area, perimeter, intensity, and shape metrics for each detected spill.
- **Severity Scores:** (If ML model is trained) probability scores for spill severity classes.

---

### Customizing for Your Project

- **Replace GitHub repo link** (`https://github.com/yourusername/OilSpillSense`) with your actual repository.
- **Add your own trained ML model** for severity classification by extending the pipeline.
- **Expand dataset** with more diverse SAR scenes for improved generalization.
- **Integrate time-series analysis** (optional) to track spill growth over multiple images.

---

### Contact

For feedback, questions, or contributions, open an issue on GitHub or reach out via the repository’s contact page.

---
```

