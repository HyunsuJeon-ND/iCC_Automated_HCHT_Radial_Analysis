# Integrated Analysis for Radial Signal Profiling in 3D Spheroids (iCC Ensemble)

This Jupyter Notebook (`Integrated Analysis for Radius Coordinate_Final.ipynb`) is designed for automated signal analysis from multichannel TIFF images of 3D tumor spheroids embedded in an inverted colloidal crystal (iCC) framework.
It collects radial intensity data from live/dead cell stains using image processing and returns CSV outputs for further analysis.

----

## Requirements
Make sure you have Python installed, along with the following packages:

- numpy 2.2.5
- pandas 2.2.3
- opencv-python 3.1.5 (cv2)  
- tifffile (2025.1.10)

Install them using pip (example):
pip install numpy pandas pillow opencv-python tifffile

---

## Input Files

- Input images must be in `.tif` format.
- The analysis assumes 3 fluorescence channels:
  - **Blue** – Live cells
  - **Green** – iCC scaffold geometry (used for ROI detection)
  - **Red** – Dead cells (or Target signal for penetration study)

---

## How to Use

1. **Set the input path and filename**  
   Modify the first cell in the notebook with your correct folder path and image filename.

2. **Adjust thresholds**  
   Set thresholds for each channel:
   - `Trs1`: Blue channel (Live)
   - `Trs2`: Green channel (ROI detection)
   - `Trs3`: Red channel (Dead)

3. **Choose the mode of analysis**  
   Set `Handle` to:
   - `1` for collecting raw intensity values  
   - `2` for collecting thresholded (binary) intensity values

---

## Included Example Images

The repository includes three example `.tif` images:
- Control (no treatment)
- Cisplatin 200 µM (24 h)
- Paclitaxel 1000 µM (24 h)

---

## Output Files

The following files will be generated with respect to each input image(*):

- Split channel images: `*_Blue_Channel.tif`, `*_Green_Channel.tif`, `*_Red_Channel.tif`
- Circle detection overlay: `*_Detected_Circles.png`
- ROI coordinates: `* HOUGH RESULT.csv`
- Individual ROIs: `/ROIs_*/(ROI#).tif`
- Raw intensity values per ROI: `/ROIs_*/(ROI#)_FIraw.csv`
- Viability values per ROI (if `Handle = 2`): `/ROIs_*/(ROI#)_Via.csv`
- Summary of ROI centroids and radii: `* centroids_and_radii.csv`
- Merged final data: `* Converged_FIraw.csv`, `* Converged_Via.csv`

---

## Notes

- This tool is optimized for spheroid ensembles formed within an iCC hydrogel framework.
- Green channel-based ROI detection is essential for accurate radial signal quantification.
