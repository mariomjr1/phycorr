# PHYCORR Pipeline
![sample](https://github.com/user-attachments/assets/e93784a6-3335-401d-ace7-b370e8843b67)

PHYCORR (Physiological Correction) contains a Matlab-based pipeline for performing R-DECO and RetroICOR analysis on physiological data. The pipeline consists of preprocessing steps to extract cardiac and respiratory signals using R-DECO, followed by the RetroICOR processing itself.

* The foundational code and functional pipeline used in this pipeline were generously provided by the Slocco Laboratory at Spaulding Rehabilitation Hospital.

## Workflow

The pipeline is executed in the following order:

1.  **Preprocessing:**
    * `preprocessing.m`: Processes raw physiological data to prepare it for peak detection.
    * **r-deco (included in repository):** Used to extract physiological peaks (e.g., R-peaks from ECG). Specifically, execute `rR_DECO.m` from the `r_deco` folder.
    * `consolidation_GUI.m`: Merges the preprocessed physiological data and the extracted peaks into a single `.mat` file.
    * `generate_1D_main_GUI_v2.m`: Generates 1D representations of the cardiac (QRS) and respiratory signals from the consolidated data. Requires `generate_1D_fun_1.m` to be in the Matlab path.
2.  **RetroICOR Processing:**
    * `retroicor.m`: Performs the RetroICOR analysis using the generated 1D signals and BOLD fMRI data.

## Detailed Instructions

### 1. Preprocessing

1.  **Run `preprocessing.m`:**
    * Execute `preprocessing.m` in Matlab.
    * Input the raw physiological data.
2.  **Extract Peaks using r-deco:**
    * Navigate to the `r_deco` folder within this repository.
    * Execute `R_DECO.m` in Matlab to identify and extract physiological peaks (e.g., R-peaks).
3.  **Run `consolidation_GUI.m`:**
    * Execute `consolidation_GUI.m` in Matlab.
    * In the GUI:
        * Select the preprocessed physiological data.
        * Select the extracted peaks from r-deco.
        * Specify an output filename for the consolidated `.mat` file.
4.  **Run `generate_1D_main_GUI_v2.m`:**
    * Ensure that `generate_1D_fun_1.m` is in the Matlab path (`addpath('path/to/generate_1D_fun_1.m')`).
    * Execute `generate_1D_main_GUI_v2.m` in Matlab.
    * In the GUI:
       * Select the folder containing the consolidated `.mat` files.
       * Specify the output file.
       * This step will generate 1D representations of the QRS and respiratory signals.

### 2. RetroICOR Processing

1.  **Add RetroICOR folder to path:**
    * Add the folder containing `retroicor.m` to the Matlab path (`addpath('path/to/retroicor')`).
2.  **Run `retroicor.m`:**
    * Execute `retroicor.m` in Matlab.
    * In the GUI:
        * Specify the folder containing the RetroICOR code.
        * Select the BOLD fMRI data in NIfTI format (from BIDS sourcedata).
        * Select the corresponding JSON file containing metadata for the BOLD data.
        * Select the 1D QRS signal generated by `generate_1D_main_GUI_v2.m`.
        * Select the 1D respiratory signal generated by `generate_1D_main_GUI_v2.m`.
        * Specify the output folder. **Note:** Due to a current issue, the output files may not be placed directly into this folder. You will need to manually move them.
3.  **Manual Output Handling:**
    * After the RetroICOR processing, manually move the output files from the default location to the specified output folder.

## Dependencies

* Matlab
* BIDS-compliant fMRI data

## Proprietary Mentions

* **RetroICOR:** This method is based on the original work by Glover et al. (2000), "Retrospective correction of physiological fluctuation in fMRI signals." NeuroImage 11, 162–175.
* **R-DECO:** This tool is based on the original work by Moeyersons, J. et al. (2020)," R-DECO: An open-source Matlab based graphical user interface for the detection and correction of R-peaks (version 1.0.0). PhysioNet. https://doi.org/10.13026/x6j7-sp58."
* This project builds upon base code and functions provided by the Slocco Laboratory at Spaulding Rehabilitation Hospital (Lizbeth Ayoub, Andrew Bolender, and Roberta Slocco). 

## Known Issues

* The `retroicor.m` script currently has a bug that prevents output files from being written directly to the specified output folder. This will be addressed in a future version.

## Future Improvements

* Fix the output folder issue in `retroicor.m`.
* Improve error handling and input validation.
* Add more detailed documentation and examples.
* Automate the movement of the output files.
