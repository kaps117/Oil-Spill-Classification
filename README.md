"""
OilSpillSense: Automated Oil Spill Detection & Severity Estimation from SAR Images

This pipeline imports Sentinel-1 SAR imagery, applies adaptive noise reduction, contrast enhancement,
segmentation, and morphological processing to detect oil spills. It also extracts quantitative
metrics (area, perimeter, intensity, shape) for each spill and (optionally) computes a severity
score using a pre-trained machine learning model. Results are saved as images and a CSV metrics table.

Instructions:
1. Clone this repository.
2. Install dependencies: `pip install opencv-python scikit-image scikit-learn numpy matplotlib pandas`
3. Place your SAR image (e.g., GeoTIFF) in the `data` folder.
4. Run: `python oil_spill_sense.py --image_path data/your_spill_image.tif`
"""

import os
import argparse
import cv2
import numpy as np
from skimage import exposure, filters, morphology, measure
import pandas as pd
import matplotlib.pyplot as plt

def parse_args():
    parser = argparse.ArgumentParser(description='OilSpillSense: SAR Oil Spill Detection & Severity Estimation')
    parser.add_argument('--image_path', type=str, required=True, help='Path to the SAR image file')
    parser.add_argument('--output_dir', type=str, default='results', help='Directory to save results')
    parser.add_argument('--verbose', action='store_true', help='Print progress and debug info')
    return parser.parse_args()

def main():
    args = parse_args()
    os.makedirs(args.output_dir, exist_ok=True)

    # 1. Load and preprocess the SAR image
    image = cv2.imread(args.image_path, cv2.IMREAD_GRAYSCALE)
    if image is None:
        print(f"Error: Could not load image at {args.image_path}")
        return

    if args.verbose:
        print("Image loaded successfully.")

    # 2. Adaptive noise reduction (Non-local Means Denoising)
    denoised = cv2.fastNlMeansDenoising(image, None, h=10, templateWindowSize=7, searchWindowSize=21)

    # 3. Contrast enhancement (CLAHE)
    clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8,8))
    enhanced = clahe.apply(denoised)

    # 4. Adaptive thresholding
    thresh = cv2.adaptiveThreshold(enhanced, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY_INV, 11, 2)

    # 5. Morphological opening to remove small artifacts
    kernel = np.ones((5,5), np.uint8)
    opened = cv2.morphologyEx(thresh, cv2.MORPH_OPEN, kernel)

    # 6. Edge detection (Canny)
    edges = cv2.Canny(opened, 100, 200)

    # 7. Label connected components (spills)
    labeled = measure.label(opened)
    regions = measure.regionprops(labeled, intensity_image=enhanced)

    # 8. Extract features for each spill
    features = []
    for region in regions:
        features.append([
            region.area,
            region.perimeter,
            region.mean_intensity,
            region.eccentricity,
        ])
    features = np.array(features)

    # (Optional) Machine learning severity scoring
    # Load a pre-trained RandomForestClassifier for severity estimation
    # Example: clf = joblib.load('severity_model.pkl')
    # severity_scores = clf.predict_proba(features)

    # 9. Save results
    plt.imshow(edges, cmap='gray')
    plt.axis('off')
    plt.savefig(f"{args.output_dir}/oil_spill_edges.png")
    plt.close()

    plt.imshow(image, cmap='gray')
    for region in regions:
        minr, minc, maxr, maxc = region.bbox
        plt.plot([minc, maxc, maxc, minc, minc], [minr, minr, maxr, maxr, minr], '-r', linewidth=1)
    plt.axis('off')
    plt.savefig(f"{args.output_dir}/oil_spill_boxes.png")
    plt.close()

    df = pd.DataFrame(features, columns=['Area (px)', 'Perimeter (px)', 'Mean Intensity', 'Eccentricity'])
    df.to_csv(f"{args.output_dir}/oil_spill_metrics.csv", index=False)

    if args.verbose:
        print("Pipeline completed successfully.")
        print(f"Results saved in {args.output_dir}")

if __name__ == "__main__":
    main()
