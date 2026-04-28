# Cumulative-Microscopy-Python
This repository contains a custom Python script designed for quantitative analysis of multiplex imaging data acquired through cumulative microscopy. The pipeline processes multi‑cycle image datasets, performs image segmentation and quantification, calculates background correction using control samples, and outputs cleaned, annotated results.

Before Running the Script
1. Image Organization
Ensure that images from different acquisition cycles are properly aligned and sorted before running the analysis.
The input directory must follow this folder structure:

SampleID/

├── c1/

├── c2/

├── c3/

└── ...

c1, c2, c3, etc. correspond to Cycle 1, Cycle 2, Cycle 3, etc.

2. Image Naming Convention

Image filenames must follow this format:

ExpID_SampleID_s1_w1.TIF

ExpID_SampleID_s1_w2.TIF

Where:

ExpID = Experiment identifier

SampleID = Sample identifier

s1 = Site (e.g., Site 1)

w1, w2, etc. = Wavelength/channel index

Example:
EXP01_F04_s1_w3.TIF

Script Configuration

PART 1 — Image Quantification

Specify input directory

dir_path = 'Your_Input_directory'

Specify output directory

dir_save = 'Your_Output_directory'

Test mode

testMode = 0    # 1 = test mode, 0 = full analysis

Use test mode (testMode = 1) to adjust segmentation parameters and visually inspect results.
Once optimal settings are defined, switch back to running mode (testMode = 0) to process the full dataset.

PART 4 — Background Calculation

Background correction is calculated using designated control samples.

Specify control samples

Ctrl_Samples = ['CS1', 'CS2', 'CS3']

Example: Ctrl_Samples = ['F04', 'E04', 'D04']

Assign control samples to cycles

Ctrl_for_cycle = ['c1:CS1', 'c2:CS2', 'c3:CS3']

Example: Ctrl_for_cycle = ['c1:F04', 'c2:E04', 'c3:D04']


PART 5 — Final Results and Column Renaming

After analysis, column names can be customized to reflect biological markers or proteins of interest.

Example column renaming:

data_file.rename(

    columns={
    
        'Int_Dapi': 'Dapi',
        
        'w2_c1': 'YourProtein1',
        
        'w3_c1': 'YourProtein2',
        
        'w4_c1': 'YourProtein3',
        
        'w2_c2': 'YourProtein4',
        
        'w3_c2': 'YourProtein5',
        
        'w4_c2': 'YourProtein6',
        
        'w2_c3': 'YourProtein7',
        
        'w3_c3': 'YourProtein8',
        
        'w4_c3': 'YourProtein9'
        
    },
    
    inplace=True
    
)

Adjust column names as needed based on:

Wavelength

Cycle number

Target protein
