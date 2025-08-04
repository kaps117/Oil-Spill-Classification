# Oil Spill Identification in SAR Imagery Using Computer Vision Techniques

This project applies computer vision methods to detect and classify oil spills in Synthetic-Aperture Radar (SAR) satellite images. By leveraging specialized image processing and segmentation techniques, the approach provides a practical way to distinguish oil spills from the surrounding sea surface, offering insights into spill extent and intensity.

## Introduction

Marine oil spills, often resulting from increased shipping activity and routine vessel operations, pose significant environmental risks. Traditional optical satellite imagery can be hindered by cloud cover or darkness, but SAR systems overcome these limitations, capturing reliable images day and night in any weather. SAR’s unique interaction with surfaces generates characteristic speckle (salt-and-pepper) noise, which complicates oil spill detection. This project develops and evaluates a series of image processing steps to improve SAR image clarity, enabling clear identification and classification of oil spills to support timely environmental response.

## Methodology

The analysis uses three diverse SAR images from the Sentinel-1 satellite, each representing different challenges for spill detection.

### Image Type 1: Noisy Image with a Concentrated Oil Spill

Salt-and-pepper noise is prominent in this image. A median filter is applied to reduce this noise, preserving edges while suppressing outliers. The resulting image is inverted to facilitate morphological operations, making the oil spill (darker than the sea) appear white. By analyzing the histogram, a threshold is chosen to segment the spill from the background. After thresholding, a morphological opening operation is used to eliminate small artifacts, retaining only significant spill regions. Finally, vertical and horizontal edge detection highlights the spill’s outline for clear visualization.

### Image Type 2: Smooth Image with Multiple Dispersed Spills

This image exhibits a smoother texture and scattered spills. The same processing pipeline as above is applied, demonstrating the robustness of the methods even when spills are distributed rather than concentrated.

### Image Type 3: Low-Contrast Image with Shallow Spill Boundaries

Here, the spill barely stands out from the sea due to low contrast. Global histogram equalization stretches the intensity range, increasing contrast and making the spill more visible. After equalization, thresholding and morphological opening are repeated to isolate the spill. Edge detection further refines the spill’s boundary.

## Results & Analysis

Each processed image demonstrates the effectiveness of tailored combinations of median filtering, histogram equalization, thresholding, morphological operations, and edge detection. The workflow successfully adapts to the varying noise levels, contrast conditions, and spill patterns found in real-world SAR images.

- **`Image Type 1`**
    
    ![image](https://user-images.githubusercontent.com/43881544/206901712-564cd93c-1181-4203-9fa0-54e7d6372bea.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901725-8c4244cb-b00f-498f-a019-85423a35080e.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901735-c3f58316-0735-4bf5-adf5-93ec502e78de.png)
    
- **`Image Type 2`**
    
    ![image](https://user-images.githubusercontent.com/43881544/206901747-082fd38b-c363-4cd1-8301-964ec640c9d3.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901752-10867337-06ad-475a-8a98-d7f54d91cb0b.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901756-0967dda3-c8d2-4ab7-9014-1f62c448d70a.png)
    
- **`Image Type 3`**
    
    ![image](https://user-images.githubusercontent.com/43881544/206901762-912c9e98-e1f8-43cf-afa5-8f138ac1307b.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901771-2d3364b4-a781-4bb0-8b0c-2399da0df8d7.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901779-d2097849-b433-45da-ba43-5760ec2609d6.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901784-41a6db0f-f8bc-41e2-be95-872ff01b5811.png)
    
    ![image](https://user-images.githubusercontent.com/43881544/206901790-e6a29034-5108-49e4-8131-f1666d011118.png)

## Conclusion

Using a combination of median filtering, average filtering, histogram equalization, intensity thresholding, edge detection, and morphological opening, this project reliably identifies oil spills in diverse SAR imagery. The methods are effective across images with high noise, smooth features, and low contrast, demonstrating both flexibility and robustness. This approach provides a practical foundation for automated oil spill monitoring using SAR data.

---
